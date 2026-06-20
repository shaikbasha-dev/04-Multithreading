03 - Multithreaded Program in Java

================================================================================
TOPIC OVERVIEW
================================================================================
A multithreaded program is a program that can execute multiple threads at the same
or nearly the same time. In Java, this allows one program to perform multiple tasks
concurrently instead of waiting for one task to finish before starting another.

Why this topic is important:
- It is the foundation of modern Java applications.
- It improves performance when tasks can run independently.
- It helps build responsive user interfaces, servers, and network applications.
- It explains the difference between sequential and concurrent execution.

================================================================================
1. DEFINITION OF MULTITHREADING
================================================================================
Multithreading is the ability of a program to create and run multiple threads in
parallel or concurrently.

A thread is a lightweight unit of execution.

In simple words:
- One program can have many threads.
- Each thread can run a different part of the program.
- Threads share the same memory space of the process.

================================================================================
2. DEFINITION OF MULTITHREADED PROGRAM
================================================================================
A multithreaded program is a Java program that uses two or more threads to execute
separate tasks.

Example idea:
- One thread prints numbers.
- Another thread prints letters.
- Both run together.

================================================================================
3. WHY MULTITHREADING IS USED
================================================================================
Multithreading is used because it helps a program:
- perform multiple tasks at the same time
- remain responsive while background tasks run
- use CPU resources efficiently
- improve speed for I/O-heavy and long-running operations

Real-life examples:
- A music player can play music while downloading songs.
- A web browser can load pages while responding to user clicks.
- A server can handle many client requests at once.

================================================================================
4. MULTITHREADING VS SINGLE-THREADING
================================================================================
Single-threaded program:
- Only one thread runs.
- Tasks execute one after another.
- Simpler to understand and debug.

Multithreaded program:
- Multiple threads run together.
- Tasks can overlap.
- More powerful but more complex.

================================================================================
5. IMPORTANT JAVA THREAD CONCEPTS
================================================================================
- Thread class
- Runnable interface
- start() method
- run() method
- sleep() method
- join() method
- synchronized keyword

================================================================================
6. HOW JVM HANDLES THREADS
================================================================================
The Java Virtual Machine (JVM) manages threads and schedules them for execution.
The operating system may run threads on different CPU cores, depending on the system.

Important point:
- The exact order of thread execution is not always fixed.
- Output order can differ from run to run.

================================================================================
7. PSEUDOCODE FOR MULTITHREADED PROGRAM
================================================================================
BEGIN
    CREATE thread T1
    CREATE thread T2

    START T1
    START T2

    WAIT for T1 to finish
    WAIT for T2 to finish

    DISPLAY "All threads completed"
END

This pseudocode shows that multiple threads can run independently.

================================================================================
8. PROGRAM 1: FIRST MULTITHREADED PROGRAM USING Thread CLASS
================================================================================
Headline:
Creating a Basic Multithreaded Program Using the Thread Class

Program:
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread running: " + i);
        }
    }
}

public class MultiThreadExample1 {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();

        System.out.println("Main thread is running");
    }
}

Why this program is used:
- It shows the easiest way to create a thread.
- It demonstrates how a new thread starts separately from the main thread.
- It helps beginners understand the relation between `Thread` and `run()`.

How this helps Java:
- It teaches the core thread model.
- It shows how Java supports concurrent execution.
- It prepares students to build more advanced multithreaded applications.

Line-by-line explanation:
1. class MyThread extends Thread {
   - Defines a custom thread class by extending Java's Thread class.

2. public void run() {
   - Defines the task that the thread will execute.

3. for (int i = 1; i <= 5; i++) {
   - Loops from 1 to 5.

4. System.out.println("Thread running: " + i);
   - Prints the current value.

5. }
   - Ends the loop.

6. }
   - Ends the run method.

7. }
   - Ends the custom class.

8. public class MultiThreadExample1 {
   - Declares the main class.

9. public static void main(String[] args) {
   - Entry point of the program.

10. MyThread t1 = new MyThread();
    - Creates an object of the custom thread.

11. t1.start();
    - Starts the thread and calls run() asynchronously.

12. System.out.println("Main thread is running");
    - Prints a message from the main thread.

13. }
    - Ends main.

14. }
    - Ends class.

Comments:
class MyThread extends Thread {
    // Custom thread class that extends Thread.
    public void run() {
        // Code to be executed by the new thread.
        for (int i = 1; i <= 5; i++) {
            // Loop runs five times.
            System.out.println("Thread running: " + i);
            // Prints the current loop count.
        }
    }
}

public class MultiThreadExample1 {
    // Main class containing the program entry point.
    public static void main(String[] args) {
        // Program starts here.
        MyThread t1 = new MyThread();
        // Creates a new thread object.
        t1.start();
        // Starts the thread so run() executes in parallel with main.
        System.out.println("Main thread is running");
        // Prints a message from the main thread.
    }
}

Output example:
Main thread is running
Thread running: 1
Thread running: 2
Thread running: 3
Thread running: 4
Thread running: 5

Summary:
This example shows how to create a simple multithreaded Java program using the Thread class.

================================================================================
9. PROGRAM 2: MULTITHREADED PROGRAM USING Runnable INTERFACE
================================================================================
Headline:
Creating Threads Using the Runnable Interface

Program:
class PrintTask implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Runnable task: " + i);
        }
    }
}

public class MultiThreadExample2 {
    public static void main(String[] args) {
        Thread t1 = new Thread(new PrintTask());
        t1.start();

        System.out.println("Main thread finished setup");
    }
}

Why this program is used:
- It demonstrates a second, more preferred way to create threads.
- It separates the task logic from thread creation.
- It is commonly used in real applications.

How this helps Java:
- It teaches object-oriented design for threading.
- It allows a class to inherit from another class while still creating a thread.
- It avoids the limitation of single inheritance.

Line-by-line explanation:
1. class PrintTask implements Runnable {
   - Declares a class that implements Runnable.

2. public void run() {
   - Defines the task to be performed by the thread.

3. for (int i = 1; i <= 5; i++) {
   - Iterates five times.

4. System.out.println("Runnable task: " + i);
   - Prints the current value.

5. }
   - Ends loop.

6. }
   - Ends run method.

7. }
   - Ends class.

8. public class MultiThreadExample2 {
   - Main class.

9. public static void main(String[] args) {
   - Entry point.

10. Thread t1 = new Thread(new PrintTask());
    - Creates a Thread object using a Runnable task.

11. t1.start();
    - Starts the thread.

12. System.out.println("Main thread finished setup");
    - Prints a message from the main thread.

13. }
    - Ends main.

14. }
    - Ends class.

Comments:
class PrintTask implements Runnable {
    // Defines a task that can be executed by a thread.
    public void run() {
        // This code runs when the thread starts.
        for (int i = 1; i <= 5; i++) {
            // Repeats five times.
            System.out.println("Runnable task: " + i);
            // Prints the value of i.
        }
    }
}

public class MultiThreadExample2 {
    // Program class.
    public static void main(String[] args) {
        // Starts execution.
        Thread t1 = new Thread(new PrintTask());
        // Creates a thread using the Runnable task.
        t1.start();
        // Starts the thread.
        System.out.println("Main thread finished setup");
        // Prints a message from the main thread.
    }
}

Output example:
Main thread finished setup
Runnable task: 1
Runnable task: 2
Runnable task: 3
Runnable task: 4
Runnable task: 5

Summary:
This example shows how to use the Runnable interface to create a multithreaded program.

================================================================================
10. PROGRAM 3: MULTITHREADING WITH TWO THREADS
================================================================================
Headline:
Running Two Threads Simultaneously

Program:
public class MultiThreadExample3 {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread 1: " + i);
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread 2: " + i);
            }
        });

        t1.start();
        t2.start();
    }
}

Why this program is used:
- It shows two threads working at the same time.
- It demonstrates concurrency clearly.
- It helps understand that thread execution order is not guaranteed.

How this helps Java:
- It teaches practical thread creation with lambda expressions.
- It shows how multiple independent tasks can be run together.
- It prepares students for real-world concurrent programs.

Line-by-line explanation:
1. public class MultiThreadExample3 {
   - Main class declaration.

2. public static void main(String[] args) {
   - Program entry point.

3. Thread t1 = new Thread(() -> {
   - Creates first thread using lambda expression.

4. for (int i = 1; i <= 5; i++) {
   - Loop for first thread.

5. System.out.println("Thread 1: " + i);
   - Prints values for thread 1.

6. }
   - Ends loop.

7. });
   - Ends lambda body.

8. Thread t2 = new Thread(() -> {
   - Creates second thread.

9. for (int i = 1; i <= 5; i++) {
   - Loop for thread 2.

10. System.out.println("Thread 2: " + i);
    - Prints values for thread 2.

11. }
    - Ends loop.

12. });
    - Ends lambda body.

13. t1.start();
    - Starts thread 1.

14. t2.start();
    - Starts thread 2.

Comments:
public class MultiThreadExample3 {
    // Program class.
    public static void main(String[] args) {
        // Main method begins execution.
        Thread t1 = new Thread(() -> {
            // Creates first thread using lambda syntax.
            for (int i = 1; i <= 5; i++) {
                // Runs five times.
                System.out.println("Thread 1: " + i);
                // Prints the value for thread 1.
            }
        });

        Thread t2 = new Thread(() -> {
            // Creates second thread.
            for (int i = 1; i <= 5; i++) {
                // Runs five times.
                System.out.println("Thread 2: " + i);
                // Prints the value for thread 2.
            }
        });

        t1.start();
        // Starts first thread.
        t2.start();
        // Starts second thread.
    }
}

Output example:
Thread 1: 1
Thread 2: 1
Thread 1: 2
Thread 2: 2
Thread 1: 3
Thread 2: 3
Thread 1: 4
Thread 2: 4
Thread 1: 5
Thread 2: 5

Summary:
This program shows two threads running together and demonstrates the concept of concurrency.

================================================================================
11. PROGRAM 4: USING sleep() METHOD
================================================================================
Headline:
Understanding Thread Sleep in Java

Program:
public class MultiThreadExample4 {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 3; i++) {
                System.out.println("Thread 1: " + i);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        t1.start();
    }
}

Why this program is used:
- It shows how to pause a thread for a short time.
- It helps understand thread scheduling and timing.
- It demonstrates exception handling in multithreading.

How this helps Java:
- It teaches practical control over execution timing.
- It helps in building applications that require delays or waiting.

Line-by-line explanation:
1. Thread.sleep(1000);
   - Pauses the thread for 1000 milliseconds.

2. catch (InterruptedException e)
   - Handles any interruption during sleep.

Comments:
public class MultiThreadExample4 {
    // Program class.
    public static void main(String[] args) {
        // Main method starts program.
        Thread t1 = new Thread(() -> {
            // Creates a thread.
            for (int i = 1; i <= 3; i++) {
                // Repeats three times.
                System.out.println("Thread 1: " + i);
                // Prints current count.
                try {
                    // Attempts to pause the thread.
                    Thread.sleep(1000);
                    // Sleeps for one second.
                } catch (InterruptedException e) {
                    // Catches interruption exception.
                    e.printStackTrace();
                    // Prints the error details.
                }
            }
        });

        t1.start();
        // Starts the thread.
    }
}

Output example:
Thread 1: 1
Thread 1: 2
Thread 1: 3

Summary:
This example shows how sleep() can pause thread execution temporarily.

================================================================================
12. COMMON PROBLEMS IN MULTITHREADING
================================================================================
- Race conditions: multiple threads access shared data at the same time.
- Deadlock: two or more threads wait forever for each other.
- Starvation: a thread never gets CPU time.
- Visibility problems: one thread may not see updated values from another thread.

================================================================================
13. WHY SYNCHRONIZATION IS IMPORTANT
================================================================================
Synchronization ensures that only one thread can access a critical section at a time.
This helps prevent inconsistent data.

Example concept:
- If two threads update the same counter at once, the result may be wrong.
- Synchronization solves this problem.

================================================================================
14. FINAL SUMMARY
================================================================================
A multithreaded program allows multiple threads to run at the same time or close to
it. Java provides built-in support for multithreading through the Thread class and
Runnable interface. Multithreading is useful for improving responsiveness and
performance, but it also introduces challenges like race conditions and deadlocks.

================================================================================
15. PROFESSIONAL NOTE FOR REPOSITORY USE
================================================================================
This topic is perfect for a GitHub repository because it covers:
- concept-based explanation
- multiple code examples
- code comments
- outputs
- comparison between single-threaded and multithreaded execution

A good folder structure would be:
- theory/
- programs/
- outputs/
- explanations/
