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


## OpenMP
### Overview,
OpenMP is a high-level API for parallel programming in C and C++. It is made up of preprocessor directives (which requires compiler support), library calls, and environment variables. OpenMP follows the fork-and-join parallel execution model, where a master thread (the initial thread) we are
working on, forks into a group of worker threads that then performed specific tasks concurrently. Upon the threads' completion of their work, the threads will synchronize at the end of the parallel block, and then execution continues with only the initial thread. Threads can do the same work, share the same tasks, or even perform distinct tasks in parallel.


OpenMP will allow programmers to separate their program into sequential and parallel regions and abstract the underlying stack memory management away, allowing users to focus on attempting to gain performance in their program via parallelization.  


OpenMP uses a shared memory model, meaning that all threads share the same address space. However, OpenMP provides the ability to declare variables private or shared within any given parallel block.


### Setup & Programming Model
To setup OpenMP within your program, please ensure that you have compiler support. Then, just include the OpenMP header file at the top of your program, by adding the line `#include <omp.h>`.


To declare a region parallel in OpenMP, you need to provide "hints" or "directives" to the compiler as to what you want to parallelize by adding a line with the general form `#pragma omp directive_name [clause_list]`. To actually declare a region parallel, use the directive_name `parallel`.


## Simple Examples
Below we will share some simple examples of various directives, showcasing the functionalities of OpenMP.


### Print the current thread running
```c
#pragma omp parallel 
{ 
	printf("Hello world, I am thread %d out of %d running threads!\n",
		omp_get_thread_num(), omp_get_num_threads()); 
}
```
`#pragma omp parallel` defines a parallel region where all threads executes the code in the following block.


### Calculating the sum of an array in parallel
```c
// sequential code
int sum = 0;
for(int i = 0; i < arr_length; i++) {
    sum += arr[i];
}


// parallelized code
#pragma omp parallel
{
	#pragma omp for reduction(+:sum)
	for(int i = 0; i < arr_length; i++) {
		sum += arr[i];
	}
}
```
