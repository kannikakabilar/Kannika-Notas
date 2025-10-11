# PyTorch
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

## (Step 3) Other ways to make a Model

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

model = models.resnet18(pretrained=True)
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

