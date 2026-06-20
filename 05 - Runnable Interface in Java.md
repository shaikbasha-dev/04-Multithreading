05 - Runnable Interface in Java

================================================================================
TOPIC OVERVIEW
================================================================================
The Runnable interface is one of the most commonly used ways to create threads in
Java. It represents a task that can be executed by a thread. Unlike extending the
Thread class, implementing Runnable allows a class to remain flexible and still be
used in object-oriented designs.

Why this topic is important:
- It is the preferred way to create threads in many real-world Java applications.
- It allows better code organization.
- It avoids the limitation of single inheritance.
- It helps build scalable and reusable multi-threaded programs.

================================================================================
1. DEFINITION OF Runnable INTERFACE
================================================================================
The Runnable interface is a functional interface in Java that contains exactly one
abstract method:

public void run()

Any class that implements Runnable must provide the body of the run() method.

================================================================================
2. WHAT IS THE run() METHOD?
================================================================================
The run() method contains the code that should be executed when the thread starts.
This is the actual task performed by the thread.

Important point:
- The run() method does not start a thread by itself.
- It only defines the task.
- To run the task in a new thread, we must create a Thread object and call start().

================================================================================
3. WHY USE Runnable INSTEAD OF EXTENDING Thread?
================================================================================
Using Runnable is preferred because:
- A class can implement Runnable and still extend another class.
- It separates task logic from thread management.
- It leads to cleaner and more reusable code.
- It is more flexible for larger applications.

================================================================================
4. BASIC CONCEPT OF THREAD CREATION WITH Runnable
================================================================================
The general flow is:
1. Create a class that implements Runnable.
2. Override the run() method.
3. Create a Thread object using the Runnable object.
4. Call start() on the Thread object.

================================================================================
5. PSEUDOCODE FOR Runnable
================================================================================
BEGIN
    CREATE class that implements Runnable
    DEFINE run() method

    CREATE Runnable object
    CREATE Thread object using Runnable object
    START thread

    DISPLAY completion message
END

================================================================================
6. PROGRAM 1: SIMPLE Runnable EXAMPLE
================================================================================
Headline:
Creating a Thread Using Runnable Interface

Program:
class MyTask implements Runnable {
    public void run() {
        System.out.println("Task is running");
    }
}

public class RunnableExample1 {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyTask());
        t1.start();
        System.out.println("Main thread is running");
    }
}

Why this program is used:
- It shows the simplest use of the Runnable interface.
- It teaches how a thread is created using a Runnable task.
- It is ideal for beginners to understand the relationship between Runnable and Thread.

How this helps Java:
- It demonstrates a clean way to define thread tasks.
- It makes the code more modular and reusable.
- It prepares students for real application development.

Line-by-line explanation:
1. class MyTask implements Runnable {
   - Creates a class that implements the Runnable interface.

2. public void run() {
   - Defines the task to be performed by the thread.

3. System.out.println("Task is running");
   - Prints a message inside the task.

4. }
   - Ends the run method.

5. }
   - Ends the class.

6. public class RunnableExample1 {
   - Declares the main class.

7. public static void main(String[] args) {
   - Entry point of the program.

8. Thread t1 = new Thread(new MyTask());
   - Creates a Thread object using the MyTask instance.

9. t1.start();
   - Starts the thread.

10. System.out.println("Main thread is running");
    - Prints a message from the main thread.

11. }
    - Ends main.

12. }
    - Ends class.

Comments:
class MyTask implements Runnable {
    // Defines a task that can be executed by a thread.
    public void run() {
        // Code of the task runs when the thread starts.
        System.out.println("Task is running");
        // Prints a message to show the task executed.
    }
}

public class RunnableExample1 {
    // Main class of the program.
    public static void main(String[] args) {
        // Execution begins here.
        Thread t1 = new Thread(new MyTask());
        // Creates a thread using the MyTask object.
        t1.start();
        // Starts the thread so run() executes.
        System.out.println("Main thread is running");
        // Prints a message from the main thread.
    }
}

Output example:
Task is running
Main thread is running

Summary:
This program shows the basic use of Runnable to execute code in a separate thread.

================================================================================
7. PROGRAM 2: Runnable WITH LOOP
================================================================================
Headline:
Running a Repeating Task Using Runnable

Program:
class LoopTask implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Loop Task: " + i);
        }
    }
}

public class RunnableExample2 {
    public static void main(String[] args) {
        Thread t1 = new Thread(new LoopTask());
        t1.start();
    }
}

Why this program is used:
- It shows how a thread can execute repeated work.
- It helps understand how loop logic works inside run().

How this helps Java:
- It demonstrates practical concurrency for repetitive tasks.
- It teaches how thread tasks can be used for iteration-based logic.

Line-by-line explanation:
1. class LoopTask implements Runnable {
   - Creates a task class.

2. public void run() {
   - Defines the task logic.

3. for (int i = 1; i <= 5; i++) {
   - Repeats five times.

4. System.out.println("Loop Task: " + i);
   - Prints the current loop value.

5. }
   - Ends the loop.

6. }
   - Ends run method.

7. }
   - Ends class.

8. public class RunnableExample2 {
   - Main class.

9. public static void main(String[] args) {
   - Entry point.

10. Thread t1 = new Thread(new LoopTask());
    - Creates thread using the LoopTask object.

11. t1.start();
    - Starts the thread.

12. }
    - Ends main.

13. }
    - Ends class.

Comments:
class LoopTask implements Runnable {
    // Defines a task that will run on a thread.
    public void run() {
        // Code that will be executed in the thread.
        for (int i = 1; i <= 5; i++) {
            // Iterates from 1 to 5.
            System.out.println("Loop Task: " + i);
            // Prints each value.
        }
    }
}

public class RunnableExample2 {
    // Class containing the program.
    public static void main(String[] args) {
        // Starts execution.
        Thread t1 = new Thread(new LoopTask());
        // Creates a new thread and passes the task.
        t1.start();
        // Starts the new thread.
    }
}

Output:
Loop Task: 1
Loop Task: 2
Loop Task: 3
Loop Task: 4
Loop Task: 5

Summary:
This program demonstrates how a Runnable task can execute a loop in a separate thread.

================================================================================
8. PROGRAM 3: USING lambda WITH Runnable
================================================================================
Headline:
Using Lambda Expression with Runnable

Program:
public class RunnableExample3 {
    public static void main(String[] args) {
        Runnable task = () -> {
            System.out.println("Lambda Runnable is running");
        };

        Thread t1 = new Thread(task);
        t1.start();
    }
}

Why this program is used:
- It shows a shorter and modern way to use Runnable.
- It helps learners understand lambda expressions in Java.

How this helps Java:
- It improves code readability.
- It simplifies thread creation for small tasks.

Line-by-line explanation:
1. Runnable task = () -> {
   - Creates a Runnable object using a lambda expression.

2. System.out.println("Lambda Runnable is running");
   - Prints a message inside the task.

3. };
   - Ends the lambda expression.

4. Thread t1 = new Thread(task);
   - Creates a thread using the task object.

5. t1.start();
   - Starts the thread.

Comments:
public class RunnableExample3 {
    // Program class.
    public static void main(String[] args) {
        // Execution starts here.
        Runnable task = () -> {
            // Defines a task using lambda expression.
            System.out.println("Lambda Runnable is running");
            // Prints a message.
        };

        Thread t1 = new Thread(task);
        // Creates a thread from the runnable task.
        t1.start();
        // Starts the thread.
    }
}

Output:
Lambda Runnable is running

Summary:
This program shows a modern and concise way to use Runnable with lambda expressions.

================================================================================
9. PROGRAM 4: Runnable WITH MULTIPLE THREADS
================================================================================
Headline:
Creating Multiple Threads Using Runnable

Program:
class Task implements Runnable {
    private String name;

    public Task(String name) {
        this.name = name;
    }

    public void run() {
        for (int i = 1; i <= 3; i++) {
            System.out.println(name + ": " + i);
        }
    }
}

public class RunnableExample4 {
    public static void main(String[] args) {
        Thread t1 = new Thread(new Task("Thread A"));
        Thread t2 = new Thread(new Task("Thread B"));

        t1.start();
        t2.start();
    }
}

Why this program is used:
- It shows how multiple Runnable tasks can run concurrently.
- It helps understand how one Runnable class can be reused for different thread instances.

How this helps Java:
- It improves scalability.
- It teaches how the same logic can run with different data.

Line-by-line explanation:
1. private String name;
   - Declares a variable to store thread name.

2. public Task(String name) {
   - Constructor assigns the name.

3. this.name = name;
   - Stores the provided name.

4. public void run() {
   - Defines the thread task.

5. for (int i = 1; i <= 3; i++) {
   - Loop runs three times.

6. System.out.println(name + ": " + i);
   - Prints the thread name and counter.

7. Thread t1 = new Thread(new Task("Thread A"));
   - Creates first thread using Task.

8. Thread t2 = new Thread(new Task("Thread B"));
   - Creates second thread using same class but different values.

9. t1.start();
   - Starts first thread.

10. t2.start();
    - Starts second thread.

Comments:
class Task implements Runnable {
    // Defines a reusable task class.
    private String name;
    // Stores the name for this task instance.

    public Task(String name) {
        // Constructor to initialize task name.
        this.name = name;
        // Assigns the value to the field.
    }

    public void run() {
        // Code executed by the thread.
        for (int i = 1; i <= 3; i++) {
            // Iterates three times.
            System.out.println(name + ": " + i);
            // Prints the thread label and value.
        }
    }
}

public class RunnableExample4 {
    // Main class.
    public static void main(String[] args) {
        // Starts execution.
        Thread t1 = new Thread(new Task("Thread A"));
        // Creates thread A.
        Thread t2 = new Thread(new Task("Thread B"));
        // Creates thread B.

        t1.start();
        // Starts thread A.
        t2.start();
        // Starts thread B.
    }
}

Output example:
Thread A: 1
Thread B: 1
Thread A: 2
Thread B: 2
Thread A: 3
Thread B: 3

Summary:
This program shows how the same Runnable implementation can be used to run multiple threads with different data.

================================================================================
10. COMMON DIFFERENCES BETWEEN Runnable AND Thread
================================================================================
Runnable:
- Better for task abstraction.
- More flexible.
- Preferred in modern Java.
- Can be used by executor services.

Thread:
- Directly represents the thread object.
- Useful for simpler examples.
- Less flexible for larger applications.

================================================================================
11. IMPORTANT POINTS TO REMEMBER
================================================================================
- Implement Runnable when you want to separate task logic from thread logic.
- Always call start() to run the task in a new thread.
- Do not call run() if you want true parallel execution.
- Lambda expressions can make Runnable code shorter.

================================================================================
12. FINAL SUMMARY
================================================================================
The Runnable interface is a powerful and preferred way to define tasks that can be
executed by threads in Java. It promotes cleaner code, flexibility, and reusability.
When combined with the Thread class, it forms the foundation for writing efficient
multithreaded programs.

================================================================================
13. PROFESSIONAL NOTE FOR REPOSITORY USE
================================================================================
This topic is ideal for a GitHub repository because it includes:
- theory and definitions
- multiple practical examples
- line-by-line explanation
- comments with each program
- sample outputs and summaries

A recommended structure is:
- theory/
- examples/
- outputs/
- notes/
