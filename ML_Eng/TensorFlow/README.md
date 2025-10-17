# TensorFlow

TensorFlow is an open-source machine learning and deep learning framework developed by Google.
It’s used to build, train, and deploy neural networks efficiently — **on CPUs, GPUs, and TPUs.**

## What is the purpose of tf.GradientTape()?

It records operations so gradients can be computed later using reverse-mode differentiation.

- TensorFlow includes Keras, a high-level API that makes model creation easy.

## Why use custom loops in TensorFlow?

To have more control — e.g., reinforcement learning, GANs, custom loss, etc.

## What are TensorFlow graphs?

A computation graph where nodes = operations, edges = tensors.

## What’s the difference between static and eager execution?

Eager = executes immediately; static = pre-builds graph first.

## What is a tensor’s rank?

The number of dimensions (e.g., scalar = rank 0, vector = rank 1).

## What’s the difference between .fit() and custom training loops?

.fit() automates training; custom loops give flexibility.

## What are callbacks?

Used to monitor training — e.g., early stopping, checkpoints, TensorBoard.

## How does TensorFlow handle distributed training?

Using tf.distribute.Strategy() (e.g., MirroredStrategy, TPUStrategy).

## Basic Example

```python
# 🧩 Step 1: Import libraries
import tensorflow as tf
import numpy as np

# 🧮 Step 2: Create training data
x = np.array([1, 2, 3, 4, 5], dtype=float)
y = np.array([3, 5, 7, 9, 11], dtype=float)  # y = 2x + 1

# 🧠 Step 3: Build the model
model = tf.keras.Sequential([
    tf.keras.layers.Dense(units=1, input_shape=[1])  # 1 neuron, 1 input
])

# ⚙️ Step 4: Compile the model
model.compile(
    optimizer='sgd',                # optimizer: how it learns
    loss='mean_squared_error'       # loss function: how it measures mistakes
)

# 🏋️ Step 5: Train the model
model.fit(x, y, epochs=500, verbose=0)  # learn over 500 epochs

# 🔮 Step 6: Make a prediction
print("Prediction for x=10.0:", model.predict([10.0]))

# 🧠 Step 7: Check learned weights and bias
weights, bias = model.layers[0].get_weights()
print("Learned Weight:", weights)
print("Learned Bias:", bias)
```

## Matrix Multiplication with Tensorflow

```python
import tensorflow as tf
matrix1 = tf.constant([[1, 2], [3, 4]])
matrix2 = tf.constant([[5, 6], [7, 8]])

result = tf.matmul(matrix1, matrix2)
print(result)
```
TensorFlow is amazing at this — because it runs the math in parallel on GPUs!

## Terms
- **Tensor Operations:** Learn how to add, multiply, reshape, and slice tensors (tf.add, tf.reshape, etc.)
- **GPU/Device Usage:** Move your code to run faster on GPU with tf.device('/GPU:0')
- **Keras API:** Build layers easily with tf.keras.Sequential() or subclassing
- **Callbacks:** Automate things like saving checkpoints and early stopping
- **Visualization:** Use TensorBoard to see loss curves and model graphs
- **Data Pipelines (tf.data):** Efficiently load and batch your data

## MNIST Classifier Tensorflow Example

```python
# Step 1: Import libraries
import tensorflow as tf
from tensorflow import keras
import matplotlib.pyplot as plt

# Step 2: Load the MNIST dataset
(x_train, y_train), (x_test, y_test) = keras.datasets.mnist.load_data()

# Step 3: Normalize (scale) the data
x_train = x_train / 255.0
x_test = x_test / 255.0

# Optional: show one sample image
plt.imshow(x_train[0], cmap='gray')
plt.title(f"Label: {y_train[0]}")
plt.show()

# Step 4: Build the model
model = keras.Sequential([
    keras.layers.Flatten(input_shape=(28, 28)),   # Flatten image (28x28 → 784)
    keras.layers.Dense(128, activation='relu'),   # Hidden layer
    keras.layers.Dense(10, activation='softmax')  # Output: 10 digits (0–9)
])

# Step 5: Compile the model
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

# Step 6: Train the model
model.fit(x_train, y_train, epochs=5)

# Step 7: Evaluate on test data
test_loss, test_acc = model.evaluate(x_test, y_test)
print(f"✅ Test Accuracy: {test_acc:.4f}")

# Step 8: Make a prediction
predictions = model.predict(x_test)

# Show example
import numpy as np
index = 0  # change to see different predictions
plt.imshow(x_test[index], cmap='gray')
plt.title(f"Predicted: {np.argmax(predictions[index])}, Actual: {y_test[index]}")
plt.show()
```

## CNN MNIST Classifier

```python
# Step 1: Import libraries
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers
import matplotlib.pyplot as plt
import numpy as np

# Step 2: Load and prepare data
(x_train, y_train), (x_test, y_test) = keras.datasets.mnist.load_data()

# CNNs need images with a channel dimension (grayscale = 1 channel)
x_train = x_train.reshape(-1, 28, 28, 1).astype("float32") / 255.0
x_test = x_test.reshape(-1, 28, 28, 1).astype("float32") / 255.0

# Step 3: Build a CNN model
model = keras.Sequential([
    layers.Conv2D(32, (3,3), activation='relu', input_shape=(28,28,1)),  # 32 filters, 3x3 window
    layers.MaxPooling2D((2,2)),  # Reduce image size
    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D((2,2)),
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')  # 10 outputs for 0–9
])

# Step 4: Compile the model
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

# Step 5: Train the model
history = model.fit(x_train, y_train, epochs=5, validation_data=(x_test, y_test))

# Step 6: Evaluate on test data
test_loss, test_acc = model.evaluate(x_test, y_test)
print(f"✅ Test Accuracy: {test_acc:.4f}")

# Step 7: Plot training progress
plt.plot(history.history['accuracy'], label='Train Accuracy')
plt.plot(history.history['val_accuracy'], label='Test Accuracy')
plt.title("Model Accuracy Over Time")
plt.xlabel("Epoch")
plt.ylabel("Accuracy")
plt.legend()
plt.show()

# Step 8: Make predictions
predictions = model.predict(x_test)

# Show a few predictions
for i in range(5):
    plt.imshow(x_test[i].reshape(28,28), cmap='gray')
    plt.title(f"Predicted: {np.argmax(predictions[i])}, Actual: {y_test[i]}")
    plt.show()
```

- **tf.image**	Resize, flip, rotate, or adjust images
- **ImageDataGenerator**	Load and augment images easily
- **tf.keras.preprocessing.image_dataset_from_directory()**	Load image folders

## Text — Language like a human!
Text → Numbers → Patterns → Meaning.

TensorFlow can turn words into vectors (number lists that capture meaning), then feed them into models like RNNs, LSTMs, or Transformers (used in ChatGPT!).

**Sentiment analysis example**
```python
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras import layers, models

sentences = ["I love TensorFlow", "I hate bugs"]
labels = [1, 0]

tokenizer = Tokenizer(num_words=100)
tokenizer.fit_on_texts(sentences)
seqs = tokenizer.texts_to_sequences(sentences)
padded = pad_sequences(seqs, padding='post')

model = models.Sequential([
    layers.Embedding(100, 16, input_length=padded.shape[1]),
    layers.LSTM(32),
    layers.Dense(1, activation='sigmoid')
])
```

- **Tokenizer**	Convert text → numbers
- **Embedding**	Learn word meanings
- **LSTM / GRU**	Remember sequences of words
- **Transformer**	Modern architecture for long texts

## Audio — Hearing like an ear!
Sound waves are numbers that vary over time. TensorFlow turns them into spectrograms (like pictures of sound) and then uses CNNs or RNNs to find patterns.

- **tf.signal.stft**	Convert audio → spectrogram
- **tensorflow_io**	Handle WAV/MP3
- **CNNs or RNNs**	Analyze sound patterns

## Tabular Data — Numbers like spreadsheets!
Each row = one example (like a customer) | Each column = one feature (like age, income, location)

**TensorFlow uses Dense layers (fully connected networks) for this.**

- **Normalization layer	Scale** inputs between 0–1
- **feature_columns**	Handle categorical (non-numeric) data
- **tf.data.Dataset**	Efficient data loading
