# A Brief Introduction to OpenMP
A parallel system is an architecture where a problem is broken into several smaller problems for multiple processors or machines. The goal of parallelization is to reduce the total runtime of a program.

This guide mainly focuses on OpenMP which is a high-level API that makes parallelizing sequential code more simple.

## Prerequisites
The following guide assumes that readers are familiar with concurrency (e.g. threads, and synchronization). If you are not familiar with these topics, we recommend checking out the following resources
- [Threads](https://en.wikipedia.org/wiki/Thread_(computing))
- [OSTEP Chapter 26](https://pages.cs.wisc.edu/~remzi/OSTEP/threads-intro.pdf)

## Shared Memory
In order to parallelize a program, threads or processes must communicate with each other. In a distributed system, they would achieve this through message passing across a network. However, we focus on parallelism on a single machine (i.e. one or more processors with one or more cores connected through shared memory). At a high-level, this simply means all processors have access to the same physical memory.

![Alt text](https://www.tutorialspoint.com/inter_process_communication/images/shared_memory.jpg)

With shared memory, processes can now communicate with each other via shared memory (implicitly). While there are libraries like pthreads that enable us to parallelize code using the shared memory paradigm, OpenMP is a higher-level abstraction that makes writing parallel code simpler (as seen in later examples). In particular, minimal changes need to be made to the sequential code to achieve parallelism.


## Limitations
As mentioned in the overview, the goal of writing parallel code is to achieve some speedup. However, there are several reasons why the speedup we achieve will not be perfect (e.g. parallelizing code on $P$ processors will not necessarily reduce the runtime by a factor of $P$).

**Amdahl's Law**: Assuming that some fraction $0 \leq p \leq 1$ of the code can be parallelized while $s = 1 - p$ of the code that cannot be parallelized (e.g. for the purpose of correctness), the maximum speedup that can be achieved (regardless of the number of processor)is $1 / s$.

**Parallelization Overheads**: To ensure parallel code is correct, we may need to add synchronization (e.g. waiting for all threads after a for loop, using locks to protect shared resources, using critical sections, etc.) These synchronizations have some overhead associated with them.

**False Sharing**: False sharing happens when two processes try to use the same cache line. When process A makes a write to the cache line, it forces process B to re-fetch the same cache line, to achieve cache coherence. However, most of the time when two processes are sharing the same cache line, they don’t necessarily need to update on each other! False Sharing is bad for performance, and OpenMP does not take care of that for you.