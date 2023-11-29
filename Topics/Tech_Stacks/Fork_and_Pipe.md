## Table of Contents

#### [Introduction](#Introduction)
#### [What is Inter-process Communication (IPC)](#IPC)
#### [Fork()](#fork)
#### [Pipe()](#pipe)
#### [IPC Using  fork()  and  pipe()](#implementation)
#### [Conclusion](#conclude)

## Introduction
This guide will help you understand the usage and implementation of Inter-process Communication (IPC) in C Programming language. 
In C programming, the **`fork()`** and **`pipe()`** functions are commonly used for process creation and Inter-process Communication, respectively. Here's an introduction to each and explanation of how they can be used together.

## What is Inter-process Communication (IPC) <a name="IPC"></a>
Inter-process Communication (IPC) is a crucial mechanism provided by the operating system that allows processes to communicate with each other. This communication could involve a process letting another process know that some event has occurred or the transferring of data between processes.

## Fork()<a name="fork"></a>

 - The `fork()` function is a fundamental feature in Unix-like operating systems used to initiate a new process.
 - When `fork()` is invoked, it creates a duplicate of the calling process (that is, the "parent process"), resulting in the formation of a "child process" that runs concurrently with the parent process.
  - After the `fork()` execution, both processes will carry out the next instruction once a new child process has been started.
  - The return value of `fork()` is an integer. It is usually employed to distinguish between the parent and child processes. The child process will receive a value of 0 returned by the `fork()` call, while the parent receives the child's process ID (PID).
 - The child process inherits the same memory contents, CPU registers, program counter, and open files from the parent process.
 - Both child and parent have the same files open at the same position. 
    -   Since they are sharing file handles, changes to the file offset made by the parent/child will be reflected in the child/parent.
> To learn more, please visit the [fork() man page](https://man7.org/linux/man-pages/man2/fork.2.html).

## Pipe()<a name="pipe"></a>
- A pipe can be used for one-way communication. It begins by opening a pipe, which acts as virtual files in main memory. This pipe can be written to by one process, and read from by another process that is connected to it.
-   The `pipe()` system call creates a pipe and places two file descriptors, one for the **read-only** end (_fildes_[0]), and the other for the **write-only** end (_fildes_[1]).
-   Data written to the pipe's write end is instantly available at the read end, with memory buffering ensuring efficient data transfer.
- Reading from an empty pipe pauses the process until data is written into it.
> To learn more, please visit the [pipe() man page](https://man7.org/linux/man-pages/man2/pipe.2.html).

## IPC Using  `fork()`  and  `pipe()`<a name="implementation"></a>

1. Before calling  `fork()`,  the parent creates a pipe object by calling pipe().
2.  Next, it calls  `fork()`. Now both the parent and the child can write/read data through the pipe. This may cause some chaos, we will have to make this a one-way communication.
3.  After  `fork()`,  the parent closes its copy of the read-only end and the child closes its copy of the write-only end.
4.  Now the parent can pass information to the child.

**Note:** To ensure pipe work properly, you should:  **Always be sure to close the end of pipe you aren't concerned with.** \
If the parent wants to receive data from the child, it should close pipefds[1], and the child should close pipefds[0]. When processes finish reading or writting, close related file descriptors. Otherwise, there will be undesired synchronization problems.

Below is a simple example of IPC using pipes by creating a pipe and forking a child process.
```c
# fd[0] gets the read end; pipeEnds[1] gets the write end.
int fd[2];

# create a pipe and fork a child process
pipe(fd);
int n = fork();

# child process
if (n == 0) {

  # close child writing end
  close(fd[1]);
  
  # Read some data from the pipe.
  char data[12];
  read(fd[0], data, 12);
  exit(EXIT_SUCCESS);
} 

# parent process
else {
  close(fd[0]);
  # Write some data to the pipe.
  write(fd[1], "Hi my child\n", 12);
  exit(EXIT_SUCCESS);
}
```
The parent process writes the string "Hi my child\n" to the write end of the pipe (`fd[1]`), and the child process reads 11 bytes of data from the read end of the pipe (`fd[0]`).

## Conclusion <a name="conclude"></a>
Understanding the roles of **`fork()`** and **`pipe()`** is foundational for implementing effective IPC strategies in C programming. Together, these functions empower developers to create and coordinate processes seamlessly. As programmers, this unlocks the potential to design robust, responsive, and efficient multi-process applications. 

## References
 - https://www.tutorialspoint.com/what-is-interprocess-communication
 - https://www.javatpoint.com/c-program-to-demonstrate-fork-and-pipe
 - https://ops-class.org/slides/2017-02-10-forksynch/
 - http://www.cse.cuhk.edu.hk/~ericlo/teaching/os/lab/6-IPC1/pipe-fork.html
