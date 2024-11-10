# Machine Learning Course (Master 2 Level)

## Slide 1: Introduction to Machine Learning
- **Definition**: ML as a subset of AI, where systems improve from experience without being explicitly programmed.
- **Categories**: Supervised, Unsupervised, Semi-supervised, Reinforcement Learning.
- **Applications**: Finance, healthcare, marketing, etc.
- **Mathematics**: Basic setup with input \( X \) and output \( Y \), laying groundwork for supervised and unsupervised learning.

---

## Slide 2: Supervised Learning – Problem Setup
- **Goal**: Learn a mapping function \( f : X \rightarrow Y \) from labeled data.
- **Types**: 
  - Classification (discrete \( Y \))
  - Regression (continuous \( Y \))
- **Mathematics**: Given a dataset \( \{ (x_i, y_i) \}_{i=1}^n \), minimize loss \( L(y, f(x)) \) over data.

---

## Slide 3: Linear Regression
- **Model**: \( y = X \beta + \epsilon \)
- **Mathematics**: Derivation of the Ordinary Least Squares (OLS) estimator
  - Objective: Minimize \( \sum_{i=1}^n (y_i - X_i \beta)^2 \)
  - Solution: \( \beta = (X^T X)^{-1} X^T y \)
- **Assumptions**: Linearity, independence, homoscedasticity, normality.

---

## Slide 4: Logistic Regression
- **Model**: \( P(Y=1 | X=x) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 X)}} \)
- **Mathematics**: Likelihood function and Maximum Likelihood Estimation (MLE)
  - Objective: Maximize \( L(\beta) = \prod_{i=1}^n P(Y_i | X_i, \beta) \)
  - Gradient ascent for optimization.

---

## Slide 5: Bias-Variance Tradeoff
- **Concept**: Balancing underfitting (high bias) and overfitting (high variance).
- **Mathematics**: Total error:
  \[
  E[(y - \hat{f}(x))^2] = \text{Bias}(\hat{f}(x))^2 + \text{Variance}(\hat{f}(x)) + \text{Irreducible Error}
  \]
- **Visualization**: Model complexity vs. error curves.

---

## Slide 6: Decision Trees
- **Concept**: Recursive partitioning to form decision rules.
- **Mathematics**: Define Gini impurity or entropy for classification, variance reduction for regression.
  - Gini impurity: \( \text{Gini}(t) = 1 - \sum_{k=1}^K p_k^2 \)

---

## Slide 7: Random Forests and Boosting
- **Random Forests**: Ensemble of decision trees using bagging and out-of-bag error.
- **Boosting**: Sequentially improving weak learners.
- **Mathematics**: Loss reduction in boosting.
  - **AdaBoost**: weight update rule \( w_{i}^{(t+1)} = w_{i}^{(t)} e^{\alpha \mathbb{1}(y_i \neq \hat{y}_i)} \)

---

## Slide 8: Support Vector Machines (SVM)
- **Concept**: Find a hyperplane that maximizes the margin between classes.
- **Mathematics**: Optimization problem for linearly separable data:
  - Maximize margin \( \frac{1}{||w||} \)
  - Subject to \( y_i(w \cdot x_i + b) \geq 1 \)
- **Kernel Trick**: Use of kernels for non-linear data.

---

## Slide 9: Unsupervised Learning – Clustering
- **K-Means Clustering**
  - **Mathematics**: Objective to minimize within-cluster sum of squares:
    \[
    \min \sum_{i=1}^K \sum_{x \in C_i} ||x - \mu_i||^2
    \]
- **Principal Component Analysis (PCA)**
  - **Mathematics**: Eigen decomposition on covariance matrix \( \Sigma = X^T X \) to reduce dimensionality.

---

## Slide 10: Neural Networks and Backpropagation
- **Concept**: Layers of neurons with activation functions.
- **Mathematics**: Derivation of backpropagation
  - Gradient of loss \( L(y, \hat{y}) \) with respect to weights, updating using chain rule.

---

## Slide 11: Deep Learning – Convolutional Neural Networks (CNNs)
- **Concept**: Use of convolutional layers for feature extraction.
- **Mathematics**: Convolution operation
  \[
  (f * g)(t) = \int_{-\infty}^{\infty} f(\tau) g(t - \tau) \, d\tau
  \]

---

## Slide 12: Transformers and Attention Mechanism
- **Concept**: Attention focuses on important parts of input sequence.
- **Mathematics**: Scaled Dot-Product Attention
  \[
  \text{Attention}(Q, K, V) = \text{softmax}\left( \frac{QK^T}{\sqrt{d_k}} \right) V
  \]
- **Application**: Self-attention in NLP.

---

This layout is ready for further detail and figures to illustrate the mathematical concepts.
