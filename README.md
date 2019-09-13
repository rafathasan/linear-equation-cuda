# Parallel Computing with CUDA

Harnessing the Power of the GPU (CUDA) to Accelerate Jacobi Algorithm to solving System of Linear Equation and Benchmarking the Parallel Level Speedup. The Program wrote in C and compilerd with NVIDIA CUDA Compiler.

## Hardware Config

| Model        | Architecture   | CUDA Cores|Clock speed|Memory Clock|
| ------------- |--------------:|-------|-------|-----------|
| TU106-200A-KA-A1|Turing (12nm)|1920|1365 MHz|14000 MHz(max)|

## Run Config

|Threads|Dataset|
|-|-|
|1,2,4,8,16,32|16,160,320,480,1024,1600|

## Benchmark

![](https://github.com/rafathasan/parallel-performence/blob/master/img/cuda%20(1).png)

![](https://github.com/rafathasan/parallel-performence/blob/master/img/cuda%20(2).png)

![](https://github.com/rafathasan/parallel-performence/blob/master/img/cuda%20(3).png)

## Limitations

*	Due to the GPU mechanism to throttle cores to 420 MHz while idle, It took much longer in the Performance but it preserved the ratio between different parallel levels. 
*	Due to that the GPU was using as Display Hardware by Windows Operating System, Windows keep interrupting  the program only when it take longer time to compute. This known as ‘watchdog’, also search for “Windows TDR” it is a timeout counter used by Windows to interrupt any unnecessary program running on Display Hardware. And I could not able record timing for large datasets(1600, 2080, 3200). This why Windows is not idle platform for CUDA programming.
*	Due to the large dataset the program didn’t get any benefit from shared memory across the threads, the shared memory per block is 48 Kilobytes. Thought I tested out partial shared memory performance but it didn’t give any benefit at all, because the calculation were combination of shared and global which takes same as global memory because the cores have to wait for the global memory to read at the memory clock speed. Therefore it is understandable that the whole dataset per operation need to be in the shared memory to get the speedup benefits.
