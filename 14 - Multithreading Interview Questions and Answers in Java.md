14 - Multithreading Interview Questions and Answers in Java

================================================================================
TOPIC OVERVIEW
================================================================================
This file contains important interview questions and answers related to Java
multithreading. It is designed for beginners as well as intermediate learners
who want to revise the core concepts of threads, synchronization, and concurrency.

================================================================================
1. WHAT IS MULTITHREADING?
================================================================================
Answer:
Multithreading is a feature in Java that allows multiple threads to execute
concurrently within the same program. Each thread runs independently but shares
common memory space.

Example:
class MultiThreadingDemo {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> System.out.println("Thread 1 is running"));
        Thread t2 = new Thread(() -> System.out.println("Thread 2 is running"));

        t1.start();
        t2.start();
    }
}

Explanation:
- `start()` creates a new thread and invokes the `run()` method.
- Both threads execute at the same time, depending on scheduling.

================================================================================
2. WHAT IS A THREAD?
================================================================================
Answer:
A thread is the smallest unit of execution in a program. It is a lightweight
process that allows a program to perform multiple tasks concurrently.

Example:
class ThreadExample {
    public static void main(String[] args) {
        Thread t = new Thread(() -> System.out.println("This is a thread"));
        t.start();
    }
}

================================================================================
3. DIFFERENCE BETWEEN PROCESS AND THREAD
================================================================================
Answer:
- A process is an independent program with its own memory space.
- A thread is a unit of execution inside a process and shares memory with other threads.

Example:
- A browser is a process.
- Tabs inside the browser may use threads.

================================================================================
4. WHAT IS THE DIFFERENCE BETWEEN `start()` AND `run()`?
================================================================================
Answer:
- `start()` creates a new thread and executes the code in parallel.
- `run()` simply calls the method directly on the current thread.

Example:
class StartVsRun {
    public static void main(String[] args) {
        Thread t = new Thread(() -> System.out.println("run() called"));

        t.start();
        // t.run(); // this will execute in the same thread
    }
}

================================================================================
5. HOW MANY WAYS CAN WE CREATE A THREAD?
================================================================================
Answer:
There are two common ways to create a thread in Java:
1. By extending the `Thread` class.
2. By implementing the `Runnable` interface.

Example using `Thread`:
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread class example");
    }
}

class Demo {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}

Example using `Runnable`:
class Demo2 {
    public static void main(String[] args) {
        Runnable r = () -> System.out.println("Runnable example");
        Thread t = new Thread(r);
        t.start();
    }
}

================================================================================
6. WHAT IS THE DIFFERENCE BETWEEN `Thread` AND `Runnable`?
================================================================================
Answer:
- `Thread` is a class.
- `Runnable` is an interface.
- `Runnable` is preferred because it allows better design and avoids single inheritance limitation.

Example:
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable thread running");
    }
}

class Demo3 {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}

================================================================================
7. WHAT IS THE THREAD LIFE CYCLE?
================================================================================
Answer:
A thread in Java has several states:
- New
- Runnable
- Running
- Blocked/Waiting
- Terminated

Example:
class LifeCycleDemo {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            for (int i = 0; i < 3; i++) {
                System.out.println("Running");
            }
        });

        System.out.println(t.getState());
        t.start();
        System.out.println(t.getState());
    }
}

================================================================================
8. WHAT IS SYNCHRONIZATION IN JAVA?
================================================================================
Answer:
Synchronization is used to control access to shared resources so that only one
thread can access a critical section at a time.

Example:
class Counter {
    private int count = 0;

    synchronized void increment() {
        count++;
    }

    int getCount() {
        return count;
    }
}

class SyncDemo {
    public static void main(String[] args) throws Exception {
        Counter c = new Counter();
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                c.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                c.increment();
            }
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Final count = " + c.getCount());
    }
}

================================================================================
9. WHAT IS THE DIFFERENCE BETWEEN `synchronized` METHOD AND `synchronized` BLOCK?
================================================================================
Answer:
- A synchronized method locks the entire method.
- A synchronized block locks only a specific part of code.

Example:
class Example {
    private final Object lock = new Object();

    void display() {
        synchronized (lock) {
            System.out.println("Critical section");
        }
    }
}

================================================================================
10. WHAT IS A RACE CONDITION?
================================================================================
Answer:
A race condition occurs when multiple threads access shared data at the same time
and the final result depends on the timing of thread execution.

Example:
class RaceConditionDemo {
    static int count = 0;

    public static void main(String[] args) throws Exception {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) count++;
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) count++;
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Final count = " + count);
    }
}

================================================================================
11. WHAT IS THE DIFFERENCE BETWEEN `wait()`, `notify()`, AND `notifyAll()`?
================================================================================
Answer:
- `wait()` causes a thread to wait until another thread notifies it.
- `notify()` wakes up one waiting thread.
- `notifyAll()` wakes up all waiting threads.

Example:
class SharedResource {
    private boolean flag = false;

    synchronized void produce() throws Exception {
        while (flag) {
            wait();
        }
        flag = true;
        System.out.println("Produced");
        notify();
    }

    synchronized void consume() throws Exception {
        while (!flag) {
            wait();
        }
        flag = false;
        System.out.println("Consumed");
        notify();
    }
}

================================================================================
12. WHAT IS THE DIFFERENCE BETWEEN `sleep()` AND `wait()`?
================================================================================
Answer:
- `sleep()` pauses the thread for a fixed time and does not release the lock.
- `wait()` releases the lock and waits until notified.

Example:
class SleepWaitDemo {
    public static void main(String[] args) throws Exception {
        Thread t = new Thread(() -> {
            try {
                Thread.sleep(1000);
                System.out.println("After sleep");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        t.start();
        t.join();
    }
}

================================================================================
13. WHAT IS THE `join()` METHOD USED FOR?
================================================================================
Answer:
The `join()` method allows one thread to wait for another thread to complete its execution.

Example:
class JoinDemo {
    public static void main(String[] args) throws Exception {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 3; i++) {
                System.out.println("Thread 1");
            }
        });

        t1.start();
        t1.join();
        System.out.println("Main thread continues after t1 finishes");
    }
}

================================================================================
14. WHAT IS A DAEMON THREAD?
================================================================================
Answer:
A daemon thread runs in the background and does not block the JVM from exiting.
When all non-daemon threads finish, the JVM stops running.

Example:
class DaemonDemo {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            while (true) {
                System.out.println("Daemon running");
            }
        });
        t.setDaemon(true);
        t.start();
        System.out.println("Main thread ends");
    }
}

================================================================================
15. WHAT ARE THREAD PRIORITIES?
================================================================================
Answer:
Thread priority is a hint to the scheduler about the importance of a thread.
Possible values are from `1` to `10`.

Example:
class PriorityDemo {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> System.out.println("Low priority"));
        Thread t2 = new Thread(() -> System.out.println("High priority"));

        t1.setPriority(Thread.MIN_PRIORITY);
        t2.setPriority(Thread.MAX_PRIORITY);

        t1.start();
        t2.start();
    }
}

================================================================================
16. WHAT IS THE DIFFERENCE BETWEEN `volatile` AND `synchronized`?
================================================================================
Answer:
- `volatile` ensures visibility of changes between threads.
- `synchronized` ensures both visibility and mutual exclusion.

Example:
class VolatileDemo {
    private volatile boolean running = true;

    public void stop() {
        running = false;
    }
}

================================================================================
17. WHAT IS A DEADLOCK?
================================================================================
Answer:
A deadlock occurs when two or more threads are waiting forever for each other to release resources.

Example scenario:
- Thread 1 holds Lock A and waits for Lock B.
- Thread 2 holds Lock B and waits for Lock A.

================================================================================
18. WHAT IS THE DIFFERENCE BETWEEN `ConcurrentHashMap` AND `Hashtable`?
================================================================================
Answer:
- `ConcurrentHashMap` allows concurrent access and better performance.
- `Hashtable` is synchronized and slower.

================================================================================
19. WHAT IS THE USE OF `ExecutorService`?
================================================================================
Answer:
`ExecutorService` is used to manage threads efficiently and avoid manually creating many thread objects.

Example:
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class ExecutorDemo {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        executor.submit(() -> System.out.println("Task 1"));
        executor.submit(() -> System.out.println("Task 2"));
        executor.shutdown();
    }
}

================================================================================
20. WHAT IS A THREAD SAFETY ISSUE?
================================================================================
Answer:
Thread safety means that a class or object behaves correctly when accessed by multiple threads simultaneously.

Example:
- Shared counters, shared lists, and shared variables can cause thread safety issues if not synchronized.

================================================================================
21. WHAT IS THE DIFFERENCE BETWEEN `yield()` AND `sleep()`?
================================================================================
Answer:
- `yield()` suggests that the current thread may pause to allow other threads to run.
- `sleep()` pauses the thread for a specific duration.

Example:
class YieldDemo {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            for (int i = 0; i < 3; i++) {
                System.out.println("Yielding");
                Thread.yield();
            }
        });
        t.start();
    }
}

================================================================================
22. WHAT IS THE IMPORTANCE OF INTER-THREAD COMMUNICATION?
================================================================================
Answer:
Inter-thread communication helps threads coordinate their actions and share information in a controlled manner.

Example:
- Producer-consumer pattern
- Thread signaling using `wait()` and `notify()`

================================================================================
23. WHAT IS THE PRODUCER-CONSUMER PROBLEM?
================================================================================
Answer:
The producer-consumer problem is a classic synchronization problem where one thread produces data and another thread consumes it.

Example idea:
- Producer adds items to a queue.
- Consumer removes items from the queue.

================================================================================
24. CAN WE START A THREAD TWICE?
================================================================================
Answer:
No. A thread cannot be started twice. Once a thread has started, calling `start()` again causes an exception.

Example:
class StartTwiceDemo {
    public static void main(String[] args) {
        Thread t = new Thread(() -> System.out.println("Hello"));
        t.start();
        // t.start(); // IllegalThreadStateException
    }
}

================================================================================
25. WHAT IS THE ROLE OF THE JVM IN MULTITHREADING?
================================================================================
Answer:
The JVM manages thread execution, scheduling, and memory access for Java programs. It also ensures that threads share heap memory while each thread has its own stack.

================================================================================
FINAL SUMMARY
================================================================================
Java multithreading is an important topic for interviews because it checks how well
you understand thread creation, synchronization, communication, and concurrency control.
A strong answer should include:
- thread basics
- lifecycle
- synchronization
- inter-thread communication
- thread safety
- common problems such as deadlock and race condition

================================================================================
PROFESSIONAL NOTE FOR REPOSITORY USE
================================================================================
This section is ideal for revision because it covers both theory and code examples.
It is helpful for interviews, quick practice, and GitHub-ready notes.
