# CUDA

CUDA is a platform that lets you write C/C++/Python code that runs massively in parallel on thousands of GPU cores.

## CUDA Architecture

- **Host:** The CPU and its memory (RAM).
- **Device:** The GPU and its memory (RAM).
- **Kernel:** A function that runs on the GPU in parallel.
- **Thread**
- **Block:** A group of threads that can share memory.
- **Grid:** A group of blocks that execute a kernel.

## Threads and Blocks
- Each thread executes one copy of the kernel.
- Threads are grouped into blocks, and blocks form a grid.

## Difference between CPU and GPU?
CPUs have few powerful cores; GPUs have thousands of smaller ones for parallel work.

## What is a kernel in CUDA?
A function executed in parallel by many threads on the GPU.

## What is shared memory?
A fast memory region shared by all threads in a block.

## What is coalesced memory access?
When consecutive threads access consecutive memory addresses — increases bandwidth efficiency.

## What is a warp?
A group of 32 threads that execute together on an SM (Streaming Multiprocessor).

## Difference between global and shared memory?
Global = slow, large; Shared = fast, limited, per-block.

## What is occupancy?
Ratio of active warps to maximum possible warps per SM — higher is better.

## How to profile CUDA programs?
Use nvprof or NVIDIA Nsight tools.

## Intermediate Terms
- Streams: Asynchronous kernel execution
- Pinned Memory: Faster CPU-GPU transfer
- Unified Memory: Managed memory shared between host/device
- Tensor Cores: Specialized cores for matrix math (AI workloads)
- cuBLAS / cuDNN: NVIDIA libraries for optimized math and neural nets
- PTX (Parallel Thread Execution): CUDA’s intermediate assembly code

## Numba lets you write CUDA kernels directly in Python

```python
from numba import cuda
import numpy as np

# 🧮 Step 1: Create data on CPU (host)
a = np.array([1, 2, 3, 4, 5], dtype=np.float32)
b = np.array([10, 20, 30, 40, 50], dtype=np.float32)
c = np.zeros_like(a)

# 🧠 Step 2: Define a CUDA kernel
@cuda.jit # turns the Python function into GPU code.
def add_vectors(a, b, c):
    # cuda.grid(1) gives each thread its unique index.
    i = cuda.grid(1)  # 1D index for each thread
    if i < a.size:
        c[i] = a[i] + b[i]

# ⚙️ Step 3: Copy data to GPU and launch the kernel
threads_per_block = 32
blocks_per_grid = (a.size + (threads_per_block - 1)) // threads_per_block

# launches the kernel on the GPU
add_vectors[blocks_per_grid, threads_per_block](a, b, c)

# 🖨️ Step 4: Print result (copied back to host automatically)
print("Result:", c)
# Result: [11. 22. 33. 44. 55.]
```

## Using CuPy (NumPy on the GPU)
CuPy works almost exactly like NumPy — just replace numpy with cupy
```python
import cupy as cp

# Create arrays directly on GPU
a = cp.array([1, 2, 3, 4, 5], dtype=cp.float32)
b = cp.array([10, 20, 30, 40, 50], dtype=cp.float32)

# GPU-based addition (runs in parallel)
c = a + b

# Copy result back to CPU for printing
print("Result:", c.get())
# Result: [11. 22. 33. 44. 55.]
```

## Matrix multiplication using CuPy

``python
import cupy as cp

# 🧮 Step 1: Create random matrices directly on GPU
A = cp.random.rand(4, 3, dtype=cp.float32)
B = cp.random.rand(3, 5, dtype=cp.float32)

# 🧠 Step 2: Multiply on GPU
C = cp.dot(A, B)  # or A @ B

# 🖨️ Step 3: Move result back to CPU for viewing
print("Result (A x B):\n", C.get())
# Result (A x B):
# [[0.613 0.475 0.552 0.437 0.677]
#  [0.254 0.366 0.444 0.293 0.589]
#  ...]
```
