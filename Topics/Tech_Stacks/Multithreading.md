# Multithreading

## Concepts
- Motivation for multithreading
	- Responsiveness achieved by concurrency(multi-tasking between threads)
	- Performance achieved by parallelism(multiple tasks executing in parallel)

- The thread contains
	- Stack: Region in memory, where local variables are stored, and passed into functions
	- Instruction Pointer: Address of the next instruction to execute
- Each thread is executing a different instruction and a different function at any given moment

- The threads share
	- Files
	- Heap
	- Code

- Context Switch
	- Each process has multiple threads
		- Stop thread 1
		- Schedule thread 1 out
		- Schedule thread 2 in
		- Start Thread 2
	- Each thread consumes resources in the CPU and memory
	- When we switch to a different thread
		- Store data for one thread
		- Restore data for another thread

	1. Too many threads will cause thrashing, spending more time in management than real productive work
	2. Threads consume less resources than processes
	3. Context switching between threads from the same process is cheaper than context switch between different processes

- Thread Scheduling
	- Operating system divides the time into moderately sized pieces called epochs
	- In each epochs, the operating system allocates a different time slice for each thread
	- Not all the threads get to run or complete in each epoch
	- The decision is based on Dynamic Priority = Static Priority + Bonus(can be negative)
		- Static Priority is set be the developer programmatically
		- Bonus is adjusted by the operating system in every epoch, for each thread
	- Using Dynamic Priority, the OS will give preference for interactive threads and threads that did not complete in the last epochs, or did not get enough time to run, preventing Starvation

---

## Thread and Process
- Multi-Thread
	- Multithreaded if the tasks share a lot of data
	- Threads are much faster to create an destroy
	- Switching between threads of the same process is faster(shorter context switches)
- Multi-Process
	- Security and stability are of higher importance
	- Tasks are unrelated to each other

---

## Tread Class
- Thread class: Encapsulates all thread related functionality
- Two ways to run code on a new thread
	- Implement Runnable interface, and pass to a new Thread object
	- Extend Thread class, and create an object of that class

- Thread Termination
	- Threads consume memory and kernel resources, CPU cycles and cache memory
	- If a thread finished its work, but the application is still running, we want to clean up the thread's resources
	- If a thread is misbehaving, we want to stop it
	- By default, the application will not stop as long as at least one thread is still running

- Interrupt a Thread
	- If the thread is executing a method that throws an InterruptedException
	- If the thread's code is handling the interrupt signal explicitly

- Daemon Thread
	- Background threads that do not prevent the application from exiting if the main thread terminates
		- Scenario 1: Background tasks, that should not block our application from terminating
		- Scenario 2: Code in a worker thread is not under our control, and we do not want it to block our application from terminating

- Joining Threads
	- Thread B checks and goes to sleep. When Thread A finish the work, Thread B wakes up
	- `thread.join(2000)`: 
		- Return when the thread has terminated
		- Return if the thread did not terminated under 2 seconds (time limit)
	- Do not rely on the order of execution

---

## Performance & Optimizing for Latency
- Performance criteria / definition
	- High speed trading system
		- Performance is latency (how fast / time)
	- Video Player
		- Performance is the precision and the accuracy of the frame rate
	- Machine Learning
		- Performance is the throughput (the data volume in 24 hour)
- Latency
	- The time to completion of a task. Measured in time units
		- Break one task into multiple independent tasks
		- Schedule the sub tasks to run in parallel to each other on different threads
		- Latency = T/N (N is the number of sub tasks)
	- Theoretical reduction of latency by N = performance improvement by a factor of N
	- N = ?
		- Should be as close as possible to the number of cores
		- Adding more threads than cores will be counter productive, as the additional thread will keep pushing the other threads from their core back and forth resulting in context switches, bad cache performance, and extra memory consumption
		- num of threads = num of cores is optimal only if all threads are runnable and can run without interruption (no IO / blocking calls / sleep etc) with the assumption that nothing else is running that consumes a lot of CPU
		- Hyperthreading --- Virtual Cores vs Physical Cores
	- Inherent Cost of Parallelization and Aggregation
		- Breaking task into multiple tasks
		- Thread creation, passing tasks to threads
		- Time between thread.start() to thread getting scheduled
		- Time until the last thread finishes and signals
		- Time until the aggregating thread runs
		- Aggregation of the sub-results into a single artifact
	- Can we break any task into subtasks
		- No
		- Tasks that are inherently paralyzable and can be easily broken into sub tasks
		- Unbreakable tasks that are forced to run on a single thread
		- Tasks that can be partially broken into sub tasks and partially must be run sequentially
- Throughput
	- The amount of tasks completed in a given period. Measured in tasks/time unit
	- Throughput improvement
		- Breaking tasks into subtasks
			- Latency = T/N
			- Theoretical throughput = N/T
			- Inherent Cost of Parallelization and Aggregation same as latency optimization
		- Running tasks in parallel
			- Much more likely to achieve N/T throughput by reducing the latency of execution of each individual task
	- Thread Pooling
		- Create the threads once and reusing them for future tasks instead of recreating the threads each and every time from scratch
		- Once the threads are created, they sit in the pool and the tasks are distributed among the threads through a queue
		- Each thread is taking task from the queue whenever the thread is available
		- If all the threads are busy, the tasks stay in the queue and wait for a thread
		- Fixed Thread Pool executor - create a thread pool with a fix number of threads and comes with a built in queue

---

## Sharing Data Between Threads
- Stack (exclusive)
	- Memory region where
		- Methods are called
		- Arguments are passed
		- Local variables are stored
		- Local primitive types
		- Local references
	- Stack + Instruction Pointer = State of each thread's execution
	- Stack's properties
		- All variables belong to the thread executing on that stack
		- Statically allocated when the thread is created
		- The stack's size is fixed, and relatively small
		- If our calling hierarchy is too deep, we may get an StackOverflowException (Risky with recursive calls)

- Heap (shared)
	- All the threads share the data located on the heap, and can access and allocate objects on at any moment
	- What is allocated on the heap
		- Objects (anything created with the new operator)
			- String
			- Object
			- Collection
		- Members of classes (attributes)
		- Static variables
	- Heap memory management
		- governed and managed by Garbage Collector
		- Object - stay as long as we have a reference to them
		- Members of classes - exist as long as their parent object exist (same life cycle as their parents)
		- Static variables - stay forever
	- References is not Objects

- Resource sharing between threads
	- Text Editor
		- UI Thread
		- Document Saver Thread
		- Both share the document data
	- Work Queue Architecture
		- Work Dispatcher Thread
		- Queue - backed by a data structure, stored on the heap, shared resources by worker threads
		- Worker Threads
	- Database Microservice Architecture
		- Every request is handled by a different thread
		- All requests eventually becomes reads or writes from or to the database
		- The connection to the database is consider shared resource
