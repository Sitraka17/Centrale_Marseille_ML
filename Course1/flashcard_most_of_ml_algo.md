# Machine Learning Algorithms Guide

## 1. Supervised Learning

### Classification Algorithms
- **Logistic Regression**
  - Binary and multiclass classification
  - Outputs probability scores
  - Good for linearly separable data
  - Highly interpretable

- **Decision Trees**
  - Tree-based recursive partitioning
  - Can handle both numerical and categorical data
  - Prone to overfitting
  - Highly interpretable

- **Random Forest**
  - Ensemble of decision trees
  - Reduces overfitting through bagging
  - Good for high-dimensional data
  - Handles missing values well

- **Support Vector Machines (SVM)**
  - Creates optimal hyperplane for separation
  - Effective in high-dimensional spaces
  - Kernel trick for non-linear classification
  - Memory intensive for large datasets

- **K-Nearest Neighbors (KNN)**
  - Instance-based learning
  - No training phase
  - Sensitive to feature scaling
  - Computationally intensive for large datasets

- **Naive Bayes**
  - Based on Bayes' theorem
  - Assumes feature independence
  - Fast and memory efficient
  - Good for text classification

### Regression Algorithms
- **Linear Regression**
  - Simple and multiple regression
  - Assumes linear relationship
  - Sensitive to outliers
  - Highly interpretable

- **Ridge Regression (L2)**
  - Adds L2 regularization
  - Reduces overfitting
  - Handles multicollinearity
  - All features contribute

- **Lasso Regression (L1)**
  - Adds L1 regularization
  - Feature selection
  - Sparse solutions
  - Some features become zero

- **Elastic Net**
  - Combines L1 and L2 regularization
  - Benefits of both Lasso and Ridge
  - Good for high-dimensional data

## 2. Unsupervised Learning

### Clustering Algorithms
- **K-Means**
  - Partitional clustering
  - Requires number of clusters (k)
  - Sensitive to outliers
  - Works best with isotropic clusters

- **DBSCAN**
  - Density-based clustering
  - No predetermined number of clusters
  - Handles noise and outliers
  - Can find arbitrary shaped clusters

- **Hierarchical Clustering**
  - Creates tree of clusters
  - Agglomerative or divisive
  - No preset number of clusters
  - Computationally intensive

### Dimensionality Reduction
- **Principal Component Analysis (PCA)**
  - Linear dimensionality reduction
  - Preserves variance
  - Unsupervised feature selection
  - Limited to linear relationships

- **t-SNE**
  - Non-linear dimensionality reduction
  - Good for visualization
  - Preserves local structure
  - Computationally intensive

- **UMAP**
  - Faster than t-SNE
  - Better global structure preservation
  - More scalable
  - Good for visualization

## 3. Deep Learning

### Neural Networks
- **Feedforward Neural Networks**
  - Basic architecture
  - Fully connected layers
  - Universal function approximators
  - Requires large datasets

- **Convolutional Neural Networks (CNN)**
  - Specialized for grid-like data
  - Image processing
  - Feature learning
  - Translation invariant

- **Recurrent Neural Networks (RNN)**
  - Sequential data processing
  - Time series analysis
  - Natural language processing
  - Vanishing gradient problems

- **LSTM/GRU**
  - Advanced RNN architectures
  - Better at long-term dependencies
  - More stable training
  - Memory intensive

- **Transformers**
  - Attention mechanism
  - Parallel processing
  - State-of-the-art in NLP
  - Resource intensive

## 4. Ensemble Methods

- **Bagging**
  - Reduces variance
  - Parallel training
  - Random Forest is an example
  - Independent base learners

- **Boosting**
  - Reduces bias
  - Sequential training
  - XGBoost, LightGBM examples
  - Focus on hard examples

- **Stacking**
  - Meta-learning
  - Combines multiple models
  - Can improve performance
  - Computationally intensive

## 5. Reinforcement Learning

- **Q-Learning**
  - Value-based method
  - Model-free
  - Discrete action spaces
  - Table-based approach

- **Deep Q Networks (DQN)**
  - Neural network Q-learning
  - Experience replay
  - Continuous state spaces
  - Discrete action spaces

- **Policy Gradient Methods**
  - Direct policy optimization
  - Continuous action spaces
  - Can be unstable
  - REINFORCE algorithm

- **Actor-Critic Methods**
  - Combines value and policy methods
  - More stable training
  - Continuous actions
  - A3C, PPO algorithms
