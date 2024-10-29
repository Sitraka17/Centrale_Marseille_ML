# Neural Network Text Classification Tutorial: Wine Dataset with TensorFlow
## Course Overview

This tutorial will guide you through building a neural network for classifying wines using TensorFlow. We'll use the popular Wine dataset to demonstrate text classification techniques.

### Prerequisites
- Basic Python knowledge
- Basic understanding of machine learning concepts
- TensorFlow 2.x installed
- NumPy and Pandas installed

## Part 1: Environment Setup and Data Preparation

```python
import tensorflow as tf
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

# Load the Wine dataset
from sklearn.datasets import load_wine
wine_data = load_wine()
X = pd.DataFrame(wine_data.data, columns=wine_data.feature_names)
y = wine_data.target

# Split the data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Scale the features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

## Part 2: Building the Neural Network Model

```python
def create_wine_model(input_shape):
    model = tf.keras.Sequential([
        tf.keras.layers.Dense(64, activation='relu', input_shape=input_shape),
        tf.keras.layers.Dropout(0.2),
        tf.keras.layers.Dense(32, activation='relu'),
        tf.keras.layers.Dropout(0.2),
        tf.keras.layers.Dense(3, activation='softmax')  # 3 wine classes
    ])
    
    model.compile(optimizer='adam',
                 loss='sparse_categorical_crossentropy',
                 metrics=['accuracy'])
    return model

# Create and compile the model
input_shape = (X_train.shape[1],)
model = create_wine_model(input_shape)
```

## Part 3: Training the Model

```python
# Training parameters
EPOCHS = 50
BATCH_SIZE = 32

# Train the model
history = model.fit(
    X_train_scaled, 
    y_train,
    epochs=EPOCHS,
    batch_size=BATCH_SIZE,
    validation_split=0.2,
    verbose=1
)
```

## Part 4: Model Evaluation

```python
# Evaluate the model
test_loss, test_accuracy = model.evaluate(X_test_scaled, y_test)
print(f"\nTest accuracy: {test_accuracy:.4f}")

# Make predictions
predictions = model.predict(X_test_scaled)
predicted_classes = np.argmax(predictions, axis=1)
```

## Part 5: Visualization and Analysis

```python
import matplotlib.pyplot as plt

def plot_training_history(history):
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))
    
    # Accuracy plot
    ax1.plot(history.history['accuracy'], label='Training Accuracy')
    ax1.plot(history.history['val_accuracy'], label='Validation Accuracy')
    ax1.set_title('Model Accuracy')
    ax1.set_xlabel('Epoch')
    ax1.set_ylabel('Accuracy')
    ax1.legend()
    
    # Loss plot
    ax2.plot(history.history['loss'], label='Training Loss')
    ax2.plot(history.history['val_loss'], label='Validation Loss')
    ax2.set_title('Model Loss')
    ax2.set_xlabel('Epoch')
    ax2.set_ylabel('Loss')
    ax2.legend()
    
    plt.tight_layout()
    plt.show()

# Plot training history
plot_training_history(history)
```

## Part 6: Making Predictions

```python
def predict_wine(model, scaler, features):
    # Scale the features
    scaled_features = scaler.transform([features])
    
    # Make prediction
    prediction = model.predict(scaled_features)
    predicted_class = np.argmax(prediction)
    
    # Get probability
    probability = np.max(prediction)
    
    return predicted_class, probability

# Example usage
sample_features = X_test.iloc[0].values
predicted_class, probability = predict_wine(model, scaler, sample_features)
print(f"Predicted wine class: {predicted_class}")
print(f"Prediction probability: {probability:.4f}")
```

## Key Concepts Covered

1. **Data Preprocessing**
   - Feature scaling
   - Train-test splitting
   - Data normalization

2. **Model Architecture**
   - Dense layers
   - Dropout for regularization
   - Activation functions
   - Output layer design

3. **Training Process**
   - Loss functions
   - Optimizers
   - Batch size and epochs
   - Validation split

4. **Evaluation Techniques**
   - Accuracy metrics
   - Loss monitoring
   - Prediction probabilities
   - Visualization of training progress

## Exercises for Practice

1. Modify the model architecture by:
   - Adding more layers
   - Changing the number of neurons
   - Testing different activation functions

2. Experiment with hyperparameters:
   - Try different batch sizes
   - Adjust the learning rate
   - Modify the dropout rate

3. Implement additional evaluation metrics:
   - Confusion matrix
   - Precision and recall
   - F1 score

## Additional Resources

1. TensorFlow Documentation: [https://www.tensorflow.org/docs](https://www.tensorflow.org/docs)
2. Scikit-learn Wine Dataset: [https://scikit-learn.org/stable/datasets/toy_dataset.html#wine-dataset](https://scikit-learn.org/stable/datasets/toy_dataset.html#wine-dataset)
3. Neural Network Concepts: [https://www.tensorflow.org/guide/keras/sequential_model](https://www.tensorflow.org/guide/keras/sequential_model)
