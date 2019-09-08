# CUDA in Your Python: Effective Parallel Programming on the GPU
## William Horton, @hortonhearsafoo, Senior Software Engineer at Compass
---

### Why GPUs?
Good at matrix operations
Slower clocks than CPUs but many more multiprocessors containing many cores
GPU devotes more transistors to Data Processing
General Purpose GPUs: CUDA (Nvidia), APP (AMD), OpenCL (open standard, maintained by Khronos Group)
Speaker uses a lot of PySpark, MxNet

## Different Approaches to CUDA in Python

CuPy is a drop-in for NumPy that leverages CUDA cores, and is much must faster if you have the hardware. 
CuDF for Pandas, cuML for SciKitLearn. Also mostly drop-in

Beyond these drop-ins, you need to use the CUDA API. You need to understand threads, blocks, and grids. 

Threads execute CUDA code and have a thread index in up to three dimensions. Each thread works on a different piece of the data. Many operations on vectors and matrices can be split up this way.

Blocks organize groups of threads and feature fast shared memory.

Grids organize blocks.

### Numba + CUDA JIT

Numba is a just-in-time compiler for Python that works best on code that uses NumPy arrays and functions.

Get this @cuda.jit decorator that will be just-in-time compiled as CUDA machine code!

Downsides: Exception handling, context management,c omprehensions, and generators are not supported features.

numba.cuda module exposes threads and atomic operations from CUDA in Python.

Has a CUDA simulator that is great for testing. 

### PyCUDA
Write strings of CUDA in your Python code and then it compiles it and allows you to execute it.
Benefits:
- Automatic memory management
- Object cleanup
- When Python object goes out of scope, CUDA allocated memory is freed for you
- Data transfer: In, Out, and InOut...
- CUDA errors get raised as Python exceptions

### CUDA as a C/C++ Extension
Best degree of control
"Why not just use C++?"
PyTorch, TensorFlow, etc. are already doing this
Write your C++ host code, create a setup.py file that compiles your CUDA and C++ code.
Lots of options: Cython, Pyrex, Boost.python...
Cython is recommended. It's more for Python developers than C++ developers
Nvidia provies the nvcc compiler which takes CUDA C code and compiles the kernel to GPU assembly code, replaces the special syntax in the C/C++ code so it is valid C/C++ code, and optionally can use your C/C++ compiler to compile the host (CPU) code.
Makes your code more portable, but you have to do all the memory management yourself.

### How to get started
Google Colab, Kaggle Kernels are free GPUs you can access
Cloud GPU instances: AWS, GCP
Udacity: Parallel Programming course https://github.com/udacity/cs344

### Where to go next
Applying CUDA to your workflow
Parallel programming algorithms
Other kinds of devices (xPUs like TPU, FPGA through PYNQ)

