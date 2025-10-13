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
