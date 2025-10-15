# Other ML stuff that were mentioned in the JD

## Analyze how ML models compile
Compiling an ML model = building and optimizing the computational graph that defines how your model runs

- TensorFlow - Builds a static computation graph (before running)
- PyTorch 2.0+ - Introduces torch.compile() to optimize the model graph
- JAX - Uses just-in-time (JIT) compilation via XLA for max performance

### When an ML model compiles
1. Parse / Build Model: framework reads your layer definitions and builds a computation graph
2. Link Operations: connects tensors and operations (matmul, add, relu) into a directed graph
3. Optimize Graph: compiler fuses redundant operations (like combining multiply + add) and optimizes memory layout
4. Select Device: decides where each op runs — CPU, GPU, or TPU — and converts it into CUDA / OpenCL kernels
5. Generate Executable Graph: Converts the graph into low-level instructions
6. Execute: The graph is executed efficiently — possibly asynchronously on GPU

## What happens when you call model.compile() in TensorFlow?
It links together the model’s forward graph, loss, optimizer, and metrics into a trainable computation graph. 
It also prepares for execution by optimizing graph structure and device placement.

## How does PyTorch 2.0’s torch.compile() improve performance?
It captures and compiles the dynamic computation graph into an optimized static representation using TorchDynamo and Inductor, 
which fuses operations and generates efficient GPU code.

## What tools can you use to analyze model compilation?
- TensorFlow: AutoGraph, XLA Debug Dumps, TensorBoard Graphs
- PyTorch: TorchDynamo, FX Graph, Profiler, torch.compile(explain=True)

## How do you run experiments to evaluate and improve performance across devices?
1. Set Up Reproducible Environment
  - Keep:
    - Fixed random seeds
    - Same batch sizes, data loaders, and hyperparameters
2. Benchmark Execution Time and Throughput
  - Measure how long each device takes to train or infer.
3. Profile Performance
  - Identify which layers or operations are slow.
4. Optimize Performance
  - Reduce latency, increase throughput, and optimize memory usage
5. Validate Accuracy and Stability
  - Check if model accuracy is unchanged; Confirm improvements don’t harm model quality.

## How do you Improve kernels for computation and data movement?
- To improve kernels for computation and data movement, I start by profiling the workload using **PyTorch Profiler** to identify hotspots.
1. For computation efficiency, I apply techniques like kernel fusion, tiling, and mixed precision to fully utilize GPU cores and reduce kernel launch overhead.
2. For data movement, I focus on memory coalescing, shared memory reuse, and overlapping compute with data transfers using CUDA streams.
- Together, these techniques improve arithmetic intensity and minimize bandwidth bottlenecks, leading to faster execution and better hardware utilization.

# Other Generic Qs

## Tell us about a time you solved a performance issue
I think you can come up with better examples for this Q - just be prepared

## Why are you applying for a ML intern when you're enrolled in Data Science?
- I've been interested in ML for a very long time and I always follow-up with the newest ML technologies ...
- I have worked on many ML projects ...
- I have taken a lot of ML courses throughout my Bachelor's and Master's program. There's a lot of overlap between Data Science and ML.

## Why are you interested in this role?
Answer this Q by a combination of your interest in ML (the above Q) and why you want to work at Tenstorrent.

