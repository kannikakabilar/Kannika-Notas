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
