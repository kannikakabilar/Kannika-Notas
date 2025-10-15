# Other ML stuff that were mentioned in the JD

## Tell us about a time you solved a performance issue

## Why are you interested in this role?

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
1.Set Up Reproducible Environment
  -Keep:
    -Fixed random seeds
    -Same batch sizes, data loaders, and hyperparameters
2.Benchmark Execution Time and Throughput
  -Measure how long each device takes to train or infer.
3.Profile Performance
  -Identify which layers or operations are slow.
4.Optimize Performance
  -Reduce latency, increase throughput, and optimize memory usage
5.Validate Accuracy and Stability
  -Check if model accuracy is unchanged; Confirm improvements don’t harm model quality.
