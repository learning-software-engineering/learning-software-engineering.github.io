# A Brief Introduction to OpenMP
A parallel system is an architecture where a problem is broken into several smaller problems for multiple processors or machines. The goal of parallelization is to reduce the total runtime of a program.


This guide mainly focuses on OpenMP which is a high-level API that makes parallelizing sequential code more simple.


## Prerequisites
The following guide assumes that readers are familiar with concurrency (e.g. threads, and synchronization). If you are not familiar with these topics, we recommend checking out the following resources
- [Threads](https://en.wikipedia.org/wiki/Thread_(computing))
- [OSTEP Chapter 26](https://pages.cs.wisc.edu/~remzi/OSTEP/threads-intro.pdf)


## Shared Memory
In order to parallelize a program, threads/processes must communicate with each other. On a distributed system, they would achieve this through message passing across a network. We focus on parallelism on a single machine (i.e. one or more processors with one or more cores connected through shared memory). On a high-level, this simply means all processors have access to the same physical memory.

![Alt text](https://www.tutorialspoint.com/inter_process_communication/images/shared_memory.jpg)


With shared memory, processes can now communicate with each other. However, it also introduces a lot of problems when a process starts to execute concurrently! For example, what happens when two threads try to read/write to the same location? What if thread A depends on thread B, before thread A can do its work? Some of these problems are already covered by the introductions of pthreads in CSC369, however in real life, there is a cleaner alternative, OpenMP, that hides the low level primitives, to allow parallelization.




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


As you can see, minimal code is added to obtain benefits of parallelization. The `reduction(+:sum)` clause informs the compiler that `sum` uses the `+` operation to reduce variables to prevent race conditions (when 2 or more threads update data at the same time, resulting in a potentially inaccurate update).


And, the `#pragma omp for` clause will distribute the work of the loop across different threads (e.g. if `arr_length` is 1000 and there are 2 threads, the first thread will work on loop indices `i = 0, …, 499` while the second thread works on loop indices `i = 500, …, 999`).


## Limitations
As mentioned in the overview, the goal of writing parallel code is to achieve some speedup. However, there are several reasons why the speedup we achieve will not be perfect (e.g. parallelizing code on $P$ processors will not necessarily reduce the runtime by a factor of $P$).

**Amdahl's Law**: Assuming that some fraction $0 \leq p \leq 1$ of the code can be parallelized while $s = 1 - p$ of the code that cannot be parallelized (e.g. for the purpose of correctness), the maximum speedup that can be achieved (regardless of the number of processor)is $1 / s$.

**Parallelization Overheads**: To ensure parallel code is correct, we may need to add synchronization (e.g. waiting for all threads after a for loop, using locks to protect shared resources, using critical sections, etc.) These synchronizations have some overhead associated with them.

**Cache line**: Imagine you are reading a book. However every time you read a page you only read one word at a time, think about what that word means, then move on to the next word. That’s not very efficient and if there are 100 words on a page, you would read 100 times. What if we read 10 words at a time? We would only read 10 times in total. This is exactly what cache line does - if you are iterating through an array, instead of fetching the elements one at a time, multiple elements would be fetched at once. So when you move onto the next element, it’s already in memory! In programming, reading from memory is very slow compared to computation. If you use cache line to your advantage (improved spatial locality), you can make your program run many, many times faster.

**False Sharing**: False sharing happens when two processes try to use the same cache line. When process A makes a write to the cache line, it forces process B to re-fetch the same cache line, to achieve cache coherence. However, most of the time when two processes are sharing the same cache line, they don’t necessarily need to update on each other! False Sharing is bad for performance, and OpenMP does not take care of that for you.


## References
- [OpenMP Wikipedia](https://en.wikipedia.org/wiki/OpenMP)
- [OpenMP Tutorial](https://hpc-tutorials.llnl.gov/openmp/)
- [OpenMP Tutorial - tutorialspoint](https://www.tutorialspoint.com/inter_process_communication/inter_process_communication_shared_memory.htm)



