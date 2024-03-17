# A Brief Introduction to OpenMP
A parallel system is an architecture where a problem is broken into several smaller problems for multiple processors or machines. The goal of parallelization is to reduce the total runtime of a program.

This guide mainly focuses on OpenMP which is a high-level API that makes parallelizing sequential code more simple.

## Prerequisites
The following guide assumes that readers are familiar with concurrency (e.g. threads, and synchronization).

## Shared Memory
In order to parallelize a program, threads or processes must communicate with each other. In a distributed system, they would achieve this through message passing across a network. However, we focus on parallelism on a single machine (i.e. one or more processors with one or more cores connected through shared memory). At a high-level, this simply means all processors have access to the same physical memory.

![Alt text](https://www.tutorialspoint.com/inter_process_communication/images/shared_memory.jpg)

With shared memory, processes can now communicate with each other via shared memory (implicitly). While there are libraries like pthreads that enable us to parallelize code using the shared memory paradigm, OpenMP is a higher-level abstraction that makes writing parallel code simpler (as seen in later examples). In particular, minimal changes need to be made to the sequential code to achieve parallelism.