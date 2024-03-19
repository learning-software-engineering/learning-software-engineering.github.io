# Introduction to OpenMP

## Brief Overview of parallel computing and OpenMP

- Parallel computing is a type of computation in which many calculations are carried out simultaneously.
- Speedup of a parallel program, $S(p) = \frac{T(1)}{T(p)} = \frac{1}{\alpha + 1/p (1-\alpha)}$
  - p: number of processors (or cores),
  - $\alpha$: fraction of the program that is serial.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d7/Gustafson.png/300px-Gustafson.png)

- OpenMP

  OpenMP is an Application Program Interface (API) that may be used to explicitly direct *multi-threaded, shared memory parallelism* in C/C++ programs. It is not intrusive on the original serial code in that the OpenMP instructions are made in pragmas interpreted by the compiler.

- OpenMP uses the fork-join model of parallel execution. All OpenMP programs begin with a single master thread which executes sequentially until a parallel region is encountered, when it creates a team of parallel threads (FORK). When the team threads complete the parallel region, they synchronize and terminate, leaving only the master thread that executes sequentially (JOIN).

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/Fork_join.svg/220px-Fork_join.svg.png)

## OpenMP Programming

### Hello World Example

Here is a basic example showing how to parallelize a hello world program. First, the sierial version:

```C
#include <stdio.h>
int main() {
    printf( "Hello, World from just me!\n" );
    return 0;
}
```

To do this in parallel (have a series of threads print out a “Hello World!” statement), we would do the following:

```C
#include <stdio.h>
#include <omp.h>  
int main() {
    int thread_id;
    #pragma omp parallel private(thread_id)
    {
        thread_id = omp_get_thread_num();
        printf( "Hello, World from thread %d!\n", thread_id );
    }
    return 0;
}
```



### Compile and run OpenMP

```
# Compile
> gcc -fopenmp omphello.c -o omphello
# Run OpenMP programs
> export OMP_NUM_THREADS = 4 # set number of threads
> ./omphello
> time ./omphello # run and measure the time.
```



### OpenMP General Code Structure

The snippet below shows the general structure of a C/C++ program using OpenMP.

```C
#include <omp.h>
main(){
	int var1, var2, var3;
  Serial code
    ...
    
  // Beginning of parallel section.
  #pragma omp parallel private(var1, var2) shared(var3)
  {
    /* Parallel section executed by all threads */
    ...
    /* All threads join master thread and disband */
  }
  Resume serial code
  ...
    return 0;
}
```

When looking at this example you should notice a few things. First, we need to include the OpenMP header (omp.h). Second, we notice a few variables that are declared outside of the parallel region of the code. If these variables are used within the parallel region we will need to know if they are *public* or *private* variables. A variable being private means that every thread will have their own copy of this variable and that changes to that variable by one thread will not be seen by other threads. A variable defined within the parallel region will be private. On the other hand, a public variable is one that is shared between all of the threads and any changes made by one thread will be seen by all of the threads. Any read-only variables can be shared. Caution must be taken when when having multiple threads read and write to the same variable. Ensuring that this is done in the proper order avoids what are called “race conditions”.

### Parallel For Loops

OpenMP can be used to easily parallelize for loops. This can only be done when the loop iterations are independent (ie. the running of one iteration of the loop does not depend on the result of previous iterations). Here is an example of for loop:
```C
/* serial version */
for (i = 0; i < 25; i++) {
  printf("Foo");
}

/* parallel version */
#pragma omp parallel for
for (i = 0; i < 25; i++) {
  printf("Foo");
}
```

### OpenMP Directives

In the previous sections examples of OpenMP directives have been given. The general format of these directives are:

```C
#pragma omp directive-name [clause,..] newline
```

The scope of a directive is a block of statements surrounded by { }. A variety of clauses are available, including:

- if (expression): only in parallel if expression evaluates to true
- private(list): variables private and local to a thread
- shared(list): data accessed by all threads
- default (none|shared)
- reduction (operator: list)

The reduction clause is used when the result of a parallel region is single value. For example, imagine we have an array of integers we would like the sum of. We can do this in parallel as follows:

```C
int sum = 0;
#pragma omp parallel default(none) shared (n, x) \ 
  private (i) reduction(+ : sum) 
{
    for(i = 0; i < n; i++) 
        sum = sum + x(I);
}
```

Since sum is a shared variable, we must be careful to avoid race conditions surrounding it. Using a reduction clause ensures that the generated code avoids such situations.

## Other Useful Tips

### Synchronize threads in a parallel region using a barrier

Sometimes you may need all threads to wait at a certain point of your code before moving on. For example, if you build up a data structuire in parallel and then you want to perform some operations on said data structure, you need to ensure all of the threads have finished the first stage before the second can begin. To do this, enter a barrier into your code as follows:

```C
#pragma omp barrier
```

### Atomic & Critical Sections

Within a parallel region you may want to execute some code that only one thread should do at a time (eg. updating a shared variable. In these cases, you should use an atomic or critical region. These define blocks of code within a parallel region that will only be executed by one thread at a time. It is important to note that all threads will eventually run the code within the atomic/critical block. You should use an atomic block if you are executing a simple statement within the block. A critical region is used for lengthier blocks of code. Here is an example:

```C
#pragma omp parallel shared(x) 
{
    . . .

    #pragma omp atomic
    {
        x++;
    }
    . . . 

    #pragma omp critical
    {
        lengthier code involving variable x
    }
}
```

###  Useful Functions and Environment Variables

There are a handful of useful functions you may want to use with respect to OpenMP. These include:

- omp_get_num_threads(): This will return the number of parallel threads.
- omp_get_thread_num(): This will return the unique integer ID of the current thread.
- omp_set_num_threads(n): This will set the number of threads to be used in the parallel regions to n.

Explicitly setting the number of threads to be used in your code is not necessary. The same effect can be achieved by setting the environment variable OMP_NUM_THREADS.



## Citation

- https://carleton.ca/rcs/rcdc/introduction-to-openmp/
- https://www.bu.edu/tech/files/2017/09/OpenMP_2017Fall.pdf