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
