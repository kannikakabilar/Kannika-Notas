# 1. PyTorch
- PyTorch is a **machine learning and deep learning library** for Python.
- It helps computers learn from data — just like humans learn from experience.

Basic Example
```python
# Step 1: Import PyTorch
import torch

# Step 2: Create Data
x = torch.tensor([[1.0], [2.0], [3.0]])  # Here 'torch.tensor' makes small data boxes (tensors)
y = torch.tensor([[2.0], [4.0], [6.0]])
# Input (x) and Output (y)

# Step 3: Make a simple model
model = torch.nn.Linear(1, 1)
# 1 input -> 1 output

# Step 4: Pick a way to measure mistakes
loss_fn = torch.nn.MSELoss()
# This tells PyTorch how wrong the model’s answers are - MSE stands for Mean Squared Error

# Step 5: Pick a way to improve
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)
"""
This gives the model a way to get better each time it practices.
  SGD = Stochastic Gradient Descent (just means “practice and improve”).
  lr=0.01 is how fast it learns.
"""

# Step 6: Training Loop (Practice)
for epoch in range(1000):  # practice 1000 times
    y_pred = model(x)            # 1️⃣ Guess
    loss = loss_fn(y_pred, y)    # 2️⃣ See how wrong it is
    optimizer.zero_grad()        # 3️⃣ Clear old mistakes
    loss.backward()              # 4️⃣ Learn from mistakes
    optimizer.step()             # 5️⃣ Update brain

# Why call optimizer.zero_grad()?
# Because gradients accumulate by default in PyTorch.

# Step 7: Test it
print(model(torch.tensor([[4.0]])))  # Output should be 8.0
```

## (Step 2) Other ways to create Data
```
# Random numbers between 0 and 1
data2 = torch.rand(2, 3) # 2 rows, 3 columns
print(data2)
# output: tensor([[0.5312, 0.9627, 0.7485],
#        [0.4146, 0.3350, 0.5945]])

data3 = torch.arange(0, 10, 2)  # start=0, end=10, step=2
print(data3)
# output: tensor([0, 2, 4, 6, 8])

zeros = torch.zeros(3, 3) # 3 rows, 3 columns filled with zeros
ones = torch.ones(2, 4) # 2 rows, 4 columns filled with ones
print(zeros)
print(ones)

import numpy as np
np_array = np.array([[1, 2, 3], [4, 5, 6]])
tensor_from_np = torch.from_numpy(np_array)
print(tensor_from_np)

# Loading from csv using pandas
import pandas as pd
df = pd.read_csv('data.csv') # Read CSV
tensor_data = torch.tensor(df.values, dtype=torch.float32) # Turn into tensor
```

# 2. PyTorch Interview Questions

## How is PyTorch different from TensorFlow?
```
PyTorch is more dynamic (define-by-run), used more in research and easier for debugging.
TensorFlow is more for production, with tools for deployment like TensorFlow Serving and TensorFlow Lite.
```

## Tensors

Tensors: (like NumPy arrays but faster and can run on both CPU and GPU)
```
import torch
x = torch.tensor([[1, 2], [3, 4]])
print(x.shape)      # torch.Size([2, 2])
print(x.device)     # cpu

x = torch.rand(2, 3)  # random 2x3 matrix
print(x.size(), x.dtype)  # torch.Size([2, 3]) torch.float32
```

## How do you move a tensor to GPU?

```
x = x.to('cuda')
```

## AutoGrad

Engine in PyTorch that automatically computes gradients for your model’s parameters when training using backpropagation. (.backward())
It tracks operations on tensors with requires_grad=True

```python
x = torch.tensor(2.0, requires_grad=True)
y = x**2 + 3*x + 1

# in .backward() It computes gradients using the chain rule and stores them in x.grad.
y.backward()    # computes dy/dx and stores it in x.grad
print(x.grad)   # prints tensor(7.)
```

## Other Terms

- nn module (for neural networks): It’s made up of layers of interconnected neurons (also called nodes or units)
that can learn patterns from data.

- Optimizers (for training): they adjust the model's weights so it can learn from data.

## Neural Networks
What are the 3 main ways to define a model?

```python
import torch.nn as nn

# 1. Linear
model = torch.nn.Linear(1, 1)

# 2. Sequential
model = nn.Sequential(
    nn.Linear(1, 10),
    nn.ReLU(),
    nn.Linear(10, 1)
)
```
## When is a Sequential model used over a linear model in PyTorch
- Use a Sequential model when you want to stack multiple layers (e.g., Linear → ReLU → Linear) in a specific order.
- Use a Linear model when you only need a single linear transformation without any activation or additional layers.

```python
# 3. Custom
class MyModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.layer1 = nn.Linear(1, 10)
        self.relu = nn.ReLU()
        self.layer2 = nn.Linear(10, 1)
    def forward(self, x):
        return self.layer2(self.relu(self.layer1(x)))

model = MyModel()
```
## Why use a custom model?
It gives you flexibility to define complex logic (e.g., skip connections, multiple inputs).

## What are the steps to train a PyTorch model?
1. Prepare Data
2. Define Model
3. Define Loss Function
4. Define Optimizer
5. Training loop (forward → loss → backward → step)

## What is a Dataset and DataLoader?
Used to handle large datasets efficiently.
**DataLoader** allows batching, shuffling, and parallel loading for performance.
```python
from torch.utils.data import Dataset, DataLoader

class MyDataset(Dataset):
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __len__(self):
        return len(self.x)
    def __getitem__(self, idx):
        return self.x[idx], self.y[idx]

dataset = MyDataset(torch.arange(10), torch.arange(10)*2)
loader = DataLoader(dataset, batch_size=2, shuffle=True)
```
## What’s the difference between .item() and .detach()?
.item() → get Python number, .detach() → stop tracking gradients.

## What’s the use of with torch.no_grad()?
Disables gradient tracking (used during evaluation).

## How to save and load a model?
```python
torch.save(model.state_dict(), 'model.pth')
model.load_state_dict(torch.load('model.pth'))
```

## What’s the role of requires_grad?
Tells PyTorch to track computations for backprop.

## How to freeze layers in transfer learning?
Set param.requires_grad = False for specific layers.

## Uses of common Deep Learning Architectures
Be ready to discuss common ones:
- CNN (Convolutional Neural Networks) → images
- RNN / LSTM → sequences
- Transformers → text, NLP, vision
- GANs → image generation

You don’t need to code them all — just know what each is used for.

## What debugging tools or visualization tools do you use?
TensorBoard, torchsummary, matplotlib for loss plots

## How do you handle overfitting?
Dropout, weight decay, data augmentation

# 3. Advanced PyTorch

## Implementation of Sequential and Custom models

```
# deep learning
import torch.nn as nn
model = nn.Sequential(
    nn.Linear(1, 10),   # first layer: 1 input → 10 neurons 
    nn.ReLU(),          # activation function (adds "thinking" power) (lets it learn curves, not just straight lines)
    nn.Linear(10, 1)    # second layer: 10 → 1 output
)

# Create your own model
# torch.manual_seed(42)  # Fix randomness so that the same random numbers are generated every time
class MyModel(nn.Module):
    def __init__(self):
        super(MyModel, self).__init__()
        self.layer1 = nn.Linear(1, 10)
        self.relu = nn.ReLU()
        self.layer2 = nn.Linear(10, 1)

    # tells PyTorch how data flows through
    def forward(self, x):
        x = self.layer1(x)
        x = self.relu(x)
        x = self.layer2(x)
        return x

model = MyModel()
x = torch.tensor([[2.0]])
output = model(x)
print(output)  # this will print a random output unless you set the seed
# or you manually set the weights
# Set layer1 weights and bias
model.layer1.weight.data.fill_(1.0)
model.layer1.bias.data.fill_(0.0)

# Set layer2 weights and bias
model.layer2.weight.data.fill_(1.0)
model.layer2.bias.data.fill_(0.0)

```

## Activation function (nn.ReLU())

```python
nn.ReLU()  # Keeps positive numbers, makes negatives 0

nn.Sigmoid()  # Squishes between 0 and 1

nn.Tanh()  # Squishes between -1 and 1 like the tan function

nn.LeakyReLU()  # Like ReLU but doesn’t kill negatives completely

# Replace any of the above functions in below
model = nn.Sequential(
    nn.Linear(2, 5),
    nn.Tanh(),
    nn.Linear(5, 1)
)
```

## Models for Images 
When we’re working with pictures (like classifying cats 🐱 and dogs 🐶), we use Convolutional Layers — these look for patterns in small parts of the image.

```python
model = nn.Sequential(
    nn.Conv2d(1, 16, 3, stride=1, padding=1),  # look at image patches
    nn.ReLU(),
    nn.MaxPool2d(2, 2),                        # shrink size
    nn.Conv2d(16, 32, 3, stride=1, padding=1),
    nn.ReLU(),
    nn.MaxPool2d(2, 2),
    nn.Flatten(),                              # flatten for final layer
    nn.Linear(32*7*7, 10)                      # classify into 10 categories
)
```

## Models for Sequences
- If your data is a sequence (like sentences, time series, or music), you can use Recurrent Neural Networks.
- The model can remember what came before

```python
model = nn.LSTM(input_size=10, hidden_size=20, num_layers=2)
```

Full working LSTM example

```python
import torch
import torch.nn as nn

# ---------------------------
# 1. Define LSTM parameters
# ---------------------------
input_size = 10      # number of features per time step
hidden_size = 20     # number of features in hidden state
num_layers = 2       # number of stacked LSTM layers
seq_len = 5          # number of time steps
batch_size = 3       # number of sequences processed in parallel

# ---------------------------
# 2. Create the LSTM model
# ---------------------------
model = nn.LSTM(input_size=input_size, hidden_size=hidden_size, num_layers=num_layers)

# ---------------------------
# 3. Create dummy input data
# ---------------------------
# Shape: [seq_len, batch_size, input_size]
input_seq = torch.randn(seq_len, batch_size, input_size)

# ---------------------------
# 4. Run the input through the LSTM
# ---------------------------
# output: all hidden states at each time step
# hn: final hidden state for each layer
# cn: final cell state for each layer
output, (hn, cn) = model(input_seq)

# ---------------------------
# 5. Print output shapes
# ---------------------------
print("Input shape       :", input_seq.shape)   # [5, 3, 10]
print("Output shape      :", output.shape)      # [5, 3, 20]
print("Hidden state shape:", hn.shape)          # [2, 3, 20]
print("Cell state shape  :", cn.shape)          # [2, 3, 20]

# ---------------------------
# 6. Get the output from the last time step
# ---------------------------
last_output = output[-1]  # Shape: [batch_size, hidden_size]
print("Last time step output shape:", last_output.shape)  # [3, 20]

```

## Models with Pre-Trained brain

```python
from torchvision import models

model = models.resnet50(pretrained=True)
```
Now your model already knows about 1000 everyday objects (like dogs, cars, etc.). 🚗🐶
</br>

The below script runs a complete image classification pipeline using a pretrained ResNet-50 model. It's designed to take an input image (e.g., a photo of a cat or a car) and tell you what object is in the image based on the ImageNet dataset.

```python
import torch
from torchvision import models, transforms
from PIL import Image
import urllib

# ---------------------------
# 1. Load pretrained ResNet50
# ---------------------------
model = models.resnet50(pretrained=True)
model.eval()  # Set to evaluation mode

# ---------------------------------------
# 2. Load and preprocess your input image
# ---------------------------------------
image_path = "your_image.jpg"  # Replace with the path to your image
image = Image.open(image_path).convert("RGB")  # Ensure 3 channels

# Define the ImageNet preprocessing pipeline
transform = transforms.Compose([
    transforms.Resize(256),             # Resize smaller side to 256
    transforms.CenterCrop(224),         # Crop the center 224x224 region
    transforms.ToTensor(),              # Convert to tensor [C, H, W]
    transforms.Normalize(               # Normalize with ImageNet mean/std
        mean=[0.485, 0.456, 0.406],
        std=[0.229, 0.224, 0.225]
    )
])

# Apply preprocessing and add batch dimension
input_tensor = transform(image).unsqueeze(0)  # Shape: [1, 3, 224, 224]

# ---------------------------
# 3. Run inference with model
# ---------------------------
with torch.no_grad():
    output = model(input_tensor)  # output Shape: [1, 1000] (logits for ImageNet classes)

# ---------------------------------------
# 4. Convert output to predicted class
# ---------------------------------------
# Apply softmax to get probabilities
probabilities = torch.nn.functional.softmax(output[0], dim=0)

# Get the top-1 class index
predicted_index = torch.argmax(probabilities).item()

# Load ImageNet class labels
url = "https://raw.githubusercontent.com/pytorch/hub/master/imagenet_classes.txt"
imagenet_classes = urllib.request.urlopen(url).read().decode("utf-8").splitlines()

# Print the top predicted label
predicted_label = imagenet_classes[predicted_index]
print(f"Predicted class: {predicted_label}")
```

