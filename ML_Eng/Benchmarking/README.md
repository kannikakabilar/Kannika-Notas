# Benchmarking ML Models


## Simple Example: Benchmarking a Classifier on the Iris Dataset

```python
import time
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, classification_report

# Load dataset
data = load_iris()
X = data.data
y = data.target

# Split into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Initialize the model
model = RandomForestClassifier(n_estimators=100, random_state=42)

# Measure training time
start_train = time.time()
model.fit(X_train, y_train)
end_train = time.time()
training_time = end_train - start_train

# Measure prediction time
start_pred = time.time()
y_pred = model.predict(X_test)
end_pred = time.time()
prediction_time = end_pred - start_pred

# Calculate metrics
accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred, average='weighted', zero_division=0)
recall = recall_score(y_test, y_pred, average='weighted', zero_division=0)
f1 = f1_score(y_test, y_pred, average='weighted', zero_division=0)

# Display results
print("=== Benchmark Results ===")
print(f"Training time: {training_time:.4f} seconds")
print(f"Prediction time: {prediction_time:.4f} seconds")
print(f"Accuracy: {accuracy:.4f}")
print(f"Precision: {precision:.4f}")
print(f"Recall: {recall:.4f}")
print(f"F1 Score: {f1:.4f}")
print("\nDetailed Classification Report:")
print(classification_report(y_test, y_pred, zero_division=0))
```

## Simple Example extended to perform regression benchmarking, cross-validation, gpu/cpu time-profiling

```python
import time
import psutil
import numpy as np
from sklearn.datasets import load_diabetes
from sklearn.model_selection import cross_val_score, cross_val_predict, KFold
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

# Load a regression dataset
data = load_diabetes()
X = data.data
y = data.target

# Initialize the regression model
model = RandomForestRegressor(n_estimators=100, random_state=42)

# Cross-validation setup
cv = KFold(n_splits=5, shuffle=True, random_state=42)

# Monitor CPU usage
cpu_percent_before = psutil.cpu_percent(interval=None)
start_time = time.time()

# Cross-validation scoring (R^2)
cv_scores = cross_val_score(model, X, y, cv=cv, scoring='r2')
# Cross-validated predictions for full evaluation
y_pred = cross_val_predict(model, X, y, cv=cv)

end_time = time.time()
cpu_percent_after = psutil.cpu_percent(interval=None)

# Benchmark metrics
r2 = r2_score(y, y_pred)
rmse = mean_squared_error(y, y_pred, squared=False)
mae = mean_absolute_error(y, y_pred)

# Summary
print("=== Regression Benchmark Results ===")
print(f"Cross-Validation R^2 Scores: {cv_scores}")
print(f"Mean R^2 Score: {np.mean(cv_scores):.4f}")
print(f"R^2 Score (Full): {r2:.4f}")
print(f"RMSE: {rmse:.4f}")
print(f"MAE: {mae:.4f}")
print(f"Total Time: {end_time - start_time:.4f} seconds")
print(f"CPU Usage (approx.): {cpu_percent_after}%")

# Optional: GPU Benchmark (if using CuPy or cuML)
try:
    import cupy as cp
    start_gpu = cp.cuda.Event()
    end_gpu = cp.cuda.Event()
    start_gpu.record()

    # Example: dummy GPU operation (simulate GPU load)
    a = cp.random.rand(10000, 10000)
    b = cp.dot(a, a)

    end_gpu.record()
    end_gpu.synchronize()
    gpu_time = cp.cuda.get_elapsed_time(start_gpu, end_gpu) / 1000  # seconds

    print(f"Simulated GPU Time: {gpu_time:.4f} seconds")
except ImportError:
    print("CuPy not installed — GPU profiling skipped.")
```

### 1. Machine Learning Fundamentals

Expect practical, lightweight theory questions:

- What are the main steps in training an ML model?

- How do you evaluate model performance?

- Explain overfitting vs underfitting.

- How would you reduce overfitting?

- What’s the difference between batch size and learning rate?

- What happens if your training loss decreases but validation loss increases?

- How do CNNs differ from RNNs or Transformers?

### 2. Python / Framework (TensorFlow or PyTorch)

They’ll check that you can:

- Write clean, reproducible code

- Understand model compilation, training, and inference

- Debug or profile models

Sample questions:

- How do you create a simple neural network in TensorFlow / PyTorch?

- What does model.compile() or model.train() do?

- What’s the difference between torch.no_grad() and torch.autograd?

- How do you measure training time or inference latency?

- How can you save and reload a model?

- How do you move a model between CPU and GPU in PyTorch?

- How do you visualize or monitor performance in TensorFlow (TensorBoard)?

### 3. Benchmarking & Performance Analysis

This is the core of the role, so expect focused questions here.

Conceptual Questions:

- What metrics would you track to benchmark a model’s performance?
(Latency, throughput, memory usage, FLOPs, energy consumption, etc.)

- How would you benchmark a model on two different hardware platforms?

- How do you ensure fair benchmarking conditions?

- How do batch size and precision (FP32 vs FP16) affect performance?

- How do you identify where a model is bottlenecked?

- How would you optimize inference performance?

Practical / Coding-Style Questions:

- “Given a model that runs slowly, how would you debug it?”

- “How would you time training vs inference?”

- “How would you measure GPU utilization?”

💡 Mention tools like:

- PyTorch: torch.utils.benchmark, torch.cuda.synchronize()

- TensorFlow: tf.profiler, tf.function for graph optimization

- General: time, nvprof, nvidia-smi, cProfile

### 4. Optimization & Kernel Improvement

They might test your thinking on efficiency:

- What causes computation bottlenecks in ML models?

- How does data movement (CPU↔GPU) affect performance?

- How can you improve kernel execution efficiency?

- What’s the impact of tensor layout (NHWC vs NCHW)?

- What is mixed-precision training and when do you use it?

💡 You don’t need to know CUDA internals deeply, but you should understand how to profile and reduce bottlenecks.

### 5. Software Reliability & Clean Code

They may test your ability to write clean, maintainable code:

- How do you make experiments reproducible?
(Answer: fix random seeds, log versions, save configs)

- How do you organize ML experiments?

- How do you debug when a model’s output changes unexpectedly?

- How do you write unit tests for ML code?

- What’s your workflow when building an end-to-end demo?

💡 Mention tools like: pytest, argparse, GitHub Actions for automation.

### 6. Collaboration & Curiosity

They’ll likely gauge your passion and curiosity:

- What excites you about benchmarking ML models?

- What’s a project you’ve done that required optimization?

- How do you learn new frameworks or hardware concepts?

### Bonus Topics (for standout answers)

If you want to sound really strong:

- Mention familiarity with profiling tools (TensorBoard Profiler, Nsight Systems)

- Know what FP32 vs FP16 vs INT8 quantization means

- Understand data pipelines (I/O can bottleneck performance)

- Mention parallelization or batch inference to improve throughput

```python
import torch
import torch.nn as nn
import time

# Step 1: Create dummy input data
X = torch.randn(1000, 32)  # 1000 samples, 32 features

# Step 2: Define a simple model
class SimpleModel(nn.Module):
    def __init__(self):
        super(SimpleModel, self).__init__()
        self.net = nn.Sequential(
            nn.Linear(32, 64),
            nn.ReLU(),
            nn.Linear(64, 10),
            nn.Softmax(dim=1)
        )

    def forward(self, x):
        return self.net(x)

# Step 3: Create the model
model = SimpleModel()

# Step 4: Function to benchmark inference time
def benchmark(model, device, X, num_runs=100):
    model.to(device)
    X = X.to(device)

    # Warm-up (important for accurate GPU timing)
    with torch.no_grad():
        for _ in range(10):
            _ = model(X)

    torch.cuda.synchronize() if device.type == 'cuda' else None

    start = time.time()
    with torch.no_grad():
        for _ in range(num_runs):
            _ = model(X)
        if device.type == 'cuda':
            torch.cuda.synchronize()
    end = time.time()

    avg_time = (end - start) / num_runs
    print(f"{device.type.upper()} average inference time: {avg_time*1000:.3f} ms")

# Step 5: Run on CPU
benchmark(model, torch.device('cpu'), X)

# Step 6: Run on GPU (if available)
if torch.cuda.is_available():
    benchmark(model, torch.device('cuda'), X)
else:
    print("❌ GPU not available on this machine.")
```

If they ask “How would you benchmark model performance?”:

Mention inference latency, throughput, and memory usage

Explain that you’d:

Warm up GPU to avoid cold-start bias

Synchronize with torch.cuda.synchronize()

Run multiple iterations and average the results

Compare across devices or batch sizes

------------------------------------------------------------------------------------------------------------

## Write a function to calculate model accuracy.

```python
import torch
import torch.nn as nn

class Model(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc = nn.Linear(10, 2)
    def forward(self, x):
        return self.fc(x)
    # def accuracy(preds, labels):
        # return (preds.argmax(dim=1) == labels).float().mean()

model = Model()
print(model(torch.randn(1, 10)))
```
Follow-ups:
- What happens if the labels are one-hot encoded?
- How would you handle multi-label classification?

## Benchmarking and Performance Analysis

```python
import torch, time

x = torch.randn(1000, 32)
model = torch.nn.Linear(32, 64)

def benchmark(device):
    model.to(device)
    x_device = x.to(device)
    torch.cuda.synchronize() if device == 'cuda' else None

    start = time.time()
    for _ in range(100):
        _ = model(x_device)
    torch.cuda.synchronize() if device == 'cuda' else None
    print(f"{device}: {time.time() - start:.4f}s")

benchmark('cpu')
if torch.cuda.is_available(): benchmark('cuda')
```
Follow-ups:
- Why do we synchronize with torch.cuda.synchronize()?
- How would you measure throughput (samples/sec)?
- What’s the difference between latency and throughput?

### Measure memory usage during training or inference

```python
import torch
print(torch.cuda.memory_allocated() / 1e6, "MB")
```
Follow-ups:
- How can you reduce memory usage?
- How does batch size affect memory?
- What’s mixed precision training?

### Profile Model Performance

```python
with torch.profiler.profile(
    activities=[torch.profiler.ProfilerActivity.CPU, torch.profiler.ProfilerActivity.CUDA],
    record_shapes=True
) as prof:
    model(x.to('cuda'))

print(prof.key_averages().table(sort_by="cuda_time_total"))
```
Follow-ups:
- What do you look for in profiling results?
- How can you improve slow kernels?

## Optimization and Debugging

### Slow Training Loop - Why is this slow and how would you fix it?

```python
for batch in dataloader:
    X, y = batch
    preds = model(X)
    loss = loss_fn(preds, y)
    loss.backward()
    optimizer.step()
```

Answers
- Move tensors and model to GPU (.to('cuda'))
- Add optimizer.zero_grad()
- Use torch.cuda.amp.autocast() for mixed precision
- Increase batch size for better GPU utilization

### How can you make the experiment reproducible?

```python
import torch, numpy as np, random
torch.manual_seed(42)
np.random.seed(42)
random.seed(42)
torch.backends.cudnn.deterministic = True
torch.backends.cudnn.benchmark = False
```
