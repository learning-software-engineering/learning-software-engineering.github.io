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

## Thread Class
- Thread class: Encapsulates all thread related functionality
- Two ways to run code on a new thread
	- Implement Runnable interface, and pass to a new Thread object
	- Extend Thread class, and create an object of that class

Implement Runnable interface:
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Running MyRunnable");
    }

    public static void main(String[] args) {
        MyRunnable runnable = new MyRunnable();
        Thread thread = new Thread(runnable);
        thread.start();
    }
}
```

Extend Thread Class:
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Running MyThread");
    }

    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();
    }
}
```

- Thread Termination
	- Threads consume memory and kernel resources, CPU cycles and cache memory
	- If a thread finished its work, but the application is still running, we want to clean up the thread's resources
	- If a thread is misbehaving, we want to stop it
	- By default, the application will not stop as long as at least one thread is still running

```java
class TerminatingThread extends Thread {
    public void run() {
        while (!isInterrupted()) {
            // Perform work here
        }
        // Clean up code before thread ends
    }
}
```

- Interrupt a Thread
	- If the thread is executing a method that throws an InterruptedException
	- If the thread's code is handling the interrupt signal explicitly

```java
class InterruptExample extends Thread {
    public void run() {
        try {
            Thread.sleep(10000); // Sleep for 10 seconds
        } catch (InterruptedException e) {
            System.out.println("Thread interrupted");
        }
    }

    public static void main(String[] args) {
        InterruptExample thread = new InterruptExample();
        thread.start();
        thread.interrupt(); // Interrupt the thread
    }
}
```

- Daemon Thread
	- Background threads that do not prevent the application from exiting if the main thread terminates
		- Scenario 1: Background tasks, that should not block our application from terminating
		- Scenario 2: Code in a worker thread is not under our control, and we do not want it to block our application from terminating

```java
class DaemonExample extends Thread {
    public void run() {
        while (true) {
            // Perform daemon task
        }
    }

    public static void main(String[] args) {
        DaemonExample thread = new DaemonExample();
        thread.setDaemon(true); // Set as daemon thread
        thread.start();
    }
}
```

- Joining Threads
	- Thread B checks and goes to sleep. When Thread A finish the work, Thread B wakes up
	- `thread.join(2000)`: 
		- Return when the thread has terminated
		- Return if the thread did not terminated under 2 seconds (time limit)
	- Do not rely on the order of execution

```java
class JoinExample {
    public static void main(String[] args) throws InterruptedException {
        Thread threadA = new Thread(() -> {
            // Code for Thread A
        });

        Thread threadB = new Thread(() -> {
            try {
                threadA.join(2000); // Join with a timeout of 2 seconds
                // Code for Thread B after Thread A finishes or timeout occurs
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        threadA.start();
        threadB.start();
    }
}
```

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

---

## Java Usage
- Critical Sections
	- Section of code that must be protected from concurrent execution
	- No two threads can be performing those operations simultaneously
	- If thread A is executing the critical section, thread B is blocked
```java
void aggregateFunction() {
	// enter critical section
	operation1();
	operation2();
	operation3();
	// exit critical section
}
```

- Synchronized
	- Locking mechanism
	- Used to restrict access to a critical section or entire method to a single thread at a time
	- Monitor: When multiple threads are going to try to call these methods on the same object, only one thread would be able to execute either of those methods
	- Lock: restrict access only to a section instead of a entire method. We can have multiple critical sections inside one class
		- Synchronized block is Reentrant
		- A thread cannot prevent itself from entering a critical section

Monitor Method
```java
public class ClassWithCriticalSections {

	public synchronized method1() {
		...
	}

	public synchronized method2() {
		...
	}
}
```

Lock Method
```java
public class ClassWithCriticalSections {

	Object lockingObject = new Object();

	public void method1() {
	
		// Concurrent execution
		...
		
		sychronized(lockingObject) {
			
			// critical section
		}

		// Concurrent execution
		...
	}
}
```

---

## Atomic Operation
- An operation or a set of operations is considered atomic if it appears to the rest of the system as if it occurred at once
- Single step - all or nothing
- No intermediate states
- Which operations are atomic? Most are not
	- All reference assignments are atomic
		- All getters and setters
	- All assignments to primitive types are safe except long and double (64 bits)
		- Safe types: 
			- int
			- short
			- byte
			- float
			- char
			- boolean
		- long / double solution:
			- `volatile double x = 1.0;`
			- `volatile double y = 9.0;`
			- `x = y; //atomic`
	- Classes in the java.util.concurrent.atomic
		- More advanced atomic operations
- Metrics Aggregation

## Race
- Race Condition
	- Condition when multiple threads are accessing a shared resource
	- At least one thread is modifying the resource
	- The timing of threads' scheduling may cause incorrect results
	- The core of the problem is non atomic operations performed on the shared resource
- Solution
	- Identification of the critical section where the race condition is happening
	- Protection of the critical section by a synchronized block
- Data Race
	- Compiler and CPU may execute the instructions out of order to optimize performance and utilization
	- They will do so while maintaining the logical correctness of the code
	- Out of Order execution by the compiler and CPU are important features to speed up the code
	- The compiler re-arranges instructions for better
		- Branch prediction (optimized loops, "if" statements etc.)
		- Vectorization - parallel instruction execution (SIMD)
		- Prefetching instructions - better cache performance
	- CPU re-arranges instructions for better hardware units utilization
		- `x++; y++;` no dependency between the lines of code, out of order execution
		- `x = 1; y = x + 2;` dependency between the lines of code, no reordering
- Solution
	- Establish a Happens - Before semantics by one of these methods:
		- Synchronization of methods which modify shared variables
		- Declaration of shared variables with the volatile keyword

## Locking Strategies
- Coarse-Grained Locking
	- A single lock
	- Eg: use synchronized keyword on methods
		- easy to maintain
		- overkill if methods are not interfering with each other
		- in the worst case (all threads are accessing shared resources), only one thread at a time can make progress
- Fine-Grained Locking
	- Separate lock for every shared resource
	- Eg: use synchronized keyword on attribute
		- more fine grained locking strategy for more parallelism and less contention

## Deadlock
- A situation where every thread is trying to make progress, but cannot because they are waiting for another party to make a move
- Conditions
	- Mutual Exclusion - Only one thread can have exclusive access to a resource
	- Hold and Wait - At least one thread is holding a resource and is waiting for another resource
	- Non-preemptive allocation - A resource is released only after the thread is done using it
	- Circular wait - A chain of at least two threads each one is holding one resource and waiting for another resource
- Solution
	- Avoid Circular wait - Enforce a strict order in lock acquisition
		- Lock resources in the same order, everywhere
		- easy to do with a small number of locks
		- maybe hard to accomplish if there are many locks in different places
	- Other techniques
		- Deadlock detection - Watchdog
		- Thread interruption (not possible with synchronized)
		- tryLock operations (not possible with synchronized)
