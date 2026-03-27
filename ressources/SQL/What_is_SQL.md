# SQL (Structured Query Language)

SQL is the standard programming language used for defining, manipulating, and controlling data stored in a Relational Database Management System (RDBMS). It operates on a declarative paradigm: you write code to specify *what* data you want, and the database's internal query optimizer determines the most efficient way to execute the request.



---

## 1. Core Sub-languages of SQL

SQL is not just for querying; it is a comprehensive language categorized into four distinct sub-languages based on functionality:

| Category | Full Name | Purpose | Key Commands |
| :--- | :--- | :--- | :--- |
| **DDL** | Data Definition Language | Defines database schemas and the structure of objects (tables, views, indexes). | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** | Data Manipulation Language | Queries and modifies the actual data residing within the schema objects. | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **DCL** | Data Control Language | Manages security, access rights, and permissions for database users. | `GRANT`, `REVOKE` |
| **TCL** | Transaction Control Language | Manages state changes to ensure databases maintain ACID (Atomicity, Consistency, Isolation, Durability) properties. | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

---

## 2. Fundamental Relational Concepts

SQL is designed to interact with the relational model, where data is strictly organized into structures to minimize redundancy and maintain integrity.

* **Tables:** The primary storage objects, structured as grids with **columns** (attributes/data types) and **rows** (individual records).
* **Primary Key (PK):** A column (or combination of columns) that uniquely identifies each row in a table. It strictly enforces uniqueness and cannot contain null values.
* **Foreign Key (FK):** A column that creates a permanent link between two tables, enforcing referential integrity by pointing to the Primary Key of another table.
* **Indexes:** Background data structures (frequently B-Trees) created on specific columns. They drastically reduce lookup times for `SELECT` queries, though they add slight overhead to write operations (`INSERT`, `UPDATE`, `DELETE`).

---

## 3. Technical Detail: Logical Query Processing Order

While a `SELECT` query is written from top to bottom, the database engine evaluates and processes the clauses in a completely different sequence. Understanding this lexical order is critical for debugging complex joins and aggregations.



1.  **`FROM` / `JOIN`:** Identifies the baseline datasets, creates Cartesian products, and applies join conditions to merge tables.
2.  **`WHERE`:** Filters the resulting rows based on boolean conditions. (Note: You cannot use aggregate functions or `SELECT` aliases here).
3.  **`GROUP BY`:** Partitions the remaining rows into distinct groups based on common column values.
4.  **`HAVING`:** Filters the grouped records. Unlike `WHERE`, this clause *can* evaluate aggregate functions (e.g., `HAVING SUM(sales) > 1000`).
5.  **`SELECT`:** Evaluates the expressions in the select list, extracting the specific columns requested.
6.  **`DISTINCT`:** Removes duplicate rows from the result set.
7.  **`ORDER BY`:** Sorts the final output.
8.  **`LIMIT` / `OFFSET`:** Restricts the total number of rows returned to the application.

---

## 4. Code Example: Advanced Query Structure

Here is a technical example demonstrating Common Table Expressions (CTEs), `JOIN` logic, and window functions to retrieve analytical data:

```sql
-- CTE (Common Table Expression) to pre-aggregate total sales per employee
WITH EmployeeSales AS (
    SELECT 
        e.employee_id, 
        e.department_id, 
        SUM(s.sale_amount) AS total_sales
    FROM employees e
    -- Left join ensures we keep employees even if they have 0 sales
    LEFT JOIN sales s ON e.employee_id = s.employee_id
    WHERE s.sale_date >= '2025-01-01'
    GROUP BY e.employee_id, e.department_id
)

-- Main query utilizing window functions to rank performance
SELECT 
    d.department_name,
    es.employee_id,
    es.total_sales,
    -- Rank employees within their specific departments based on sales
    RANK() OVER(PARTITION BY es.department_id ORDER BY es.total_sales DESC) as dept_rank
FROM EmployeeSales es
INNER JOIN departments d ON es.department_id = d.department_id
-- Filter out anyone not in the top 3 of their department
HAVING dept_rank <= 3
ORDER BY d.department_name ASC, dept_rank ASC;
```

Would you like me to break down how to design an optimized database schema from scratch, or should we explore the architectural differences between various SQL dialects like PostgreSQL and T-SQL?



// Use DBML to define your financial database structure
// Docs: https://dbml.dbdiagram.io/docs

Enum account_status {
  active
  frozen
  closed
}

Enum transaction_type {
  deposit
  withdrawal
  transfer
  fee
  interest
}

Table customers {
  id uuid [primary key]
  first_name varchar(100) [not null]
  last_name varchar(100) [not null]
  email varchar(255) [unique, not null]
  tax_id varchar(50) [unique, note: 'SSN, TIN, or equivalent']
  kyc_verified boolean [default: false, note: 'Know Your Customer compliance flag']
  created_at timestamp [default: `now()`]
}

Table accounts {
  id uuid [primary key]
  customer_id uuid [not null]
  account_number varchar(30) [unique, not null]
  type varchar(50) [not null, note: 'e.g., Checking, Savings, Brokerage']
  balance decimal(19, 4) [default: 0.0000, note: 'High precision for accrued interest calculation']
  currency char(3) [default: 'EUR', note: 'ISO 4217 currency code']
  status account_status [default: 'active']
  created_at timestamp [default: `now()`]
}

Table transactions {
  id uuid [primary key]
  account_id uuid [not null]
  type transaction_type [not null]
  amount decimal(19, 4) [not null, note: 'Positive values for credits, negative for debits']
  running_balance decimal(19, 4) [not null, note: 'Immutable snapshot of balance after this transaction']
  reference_id uuid [note: 'Links the debit and credit legs of the same transfer']
  description text
  executed_at timestamp [default: `now()`]
}

// Relationships
Ref: accounts.customer_id > customers.id // One customer can hold multiple accounts
Ref: transactions.account_id > accounts.id // One account contains multiple ledger entries
