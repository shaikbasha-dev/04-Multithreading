09 - Sleep Method in Java

================================================================================
TOPIC OVERVIEW
================================================================================
The sleep() method is one of the most important methods in Java threading. It is
used to pause the execution of a thread for a specified amount of time. This is
helpful when a program needs to wait, delay work, or allow other threads to run.

Why this topic is important:
- It explains how to pause thread execution safely.
- It is used in many examples related to scheduling and timing.
- It helps understand how threads behave under different conditions.
- It is a key concept for interview preparation and real-world development.

================================================================================
1. DEFINITION OF sleep() METHOD
================================================================================
The sleep() method is a static method of the Thread class.

Syntax:
Thread.sleep(milliseconds)

It causes the currently executing thread to pause for the specified number of
milliseconds.

Important note:
- sleep() throws InterruptedException.
- So we must handle it using try-catch or declare throws.

================================================================================
2. WHAT DOES sleep() DO?
================================================================================
The sleep() method:
- pauses the current thread temporarily
- does not stop the thread permanently
- gives other threads a chance to execute
- helps control timing in programs

It is useful when you want the program to wait for a short period before continuing.

================================================================================
3. WHY DO WE USE sleep()?
================================================================================
We use sleep() when we want to:
- delay execution
- simulate waiting time
- allow another thread to run
- test thread scheduling behavior
- create time-based logic in applications

================================================================================
4. IMPORTANT POINTS ABOUT sleep()
================================================================================
- sleep() is a static method.
- It pauses the currently running thread only.
- The exact sleeping time may not be precise due to system scheduling.
- It throws InterruptedException.
- After sleeping, the thread resumes execution from the next statement.

================================================================================
5. PSEUDOCODE FOR sleep()
================================================================================
BEGIN
    START thread
    PRINT message
    CALL Thread.sleep(1000)
    PRINT message after sleep
END

================================================================================
6. PROGRAM 1: SIMPLE sleep() EXAMPLE
================================================================================
Headline:
Pausing Execution with Thread.sleep()

Program:
public class SleepExample1 {
    public static void main(String[] args) {
        System.out.println("Program started");

        try {
            Thread.sleep(2000);
            System.out.println("After 2 seconds");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Program finished");
    }
}

Why this program is used:
- It shows the simplest use of sleep().
- It explains how the program pauses execution for a fixed time.

How this helps Java:
- It teaches the basic concept of delaying work.
- It helps understand the importance of exception handling.

Line-by-line explanation:
1. public class SleepExample1 {
   - Declares the class.

2. public static void main(String[] args) {
   - Entry point of the program.

3. System.out.println("Program started");
   - Prints a message at the beginning.

4. try {
   - Starts a block to handle exceptions.

5. Thread.sleep(2000);
   - Pauses execution for 2000 milliseconds (2 seconds).

6. System.out.println("After 2 seconds");
   - Prints message after the pause.

7. } catch (InterruptedException e) {
   - Handles the exception thrown by sleep().

8. e.printStackTrace();
   - Prints the error details.

9. }
   - Ends the catch block.

10. System.out.println("Program finished");
    - Prints the final message.

11. }
    - Ends main.

12. }
    - Ends class.

Comments:
public class SleepExample1 {
    // Main class of the program.
    public static void main(String[] args) {
        // Program starts here.
        System.out.println("Program started");
        // Prints a message before sleeping.

        try {
            // Try block to handle possible interruption.
            Thread.sleep(2000);
            // Pauses execution for 2 seconds.
            System.out.println("After 2 seconds");
            // Prints message after waiting.
        } catch (InterruptedException e) {
            // Catches interruption exception.
            e.printStackTrace();
            // Prints error details.
        }

        System.out.println("Program finished");
        // Prints the final message.
    }
}

Output:
Program started
After 2 seconds
Program finished

Summary:
This program shows how Thread.sleep() pauses the current thread for a specific duration.

================================================================================
7. PROGRAM 2: sleep() INSIDE A THREAD
================================================================================
Headline:
Using sleep() in a Multithreaded Program

Program:
public class SleepExample2 {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 3; i++) {
                System.out.println("Thread running: " + i);
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
- It shows how sleep() works inside a thread.
- It helps understand how a thread can pause between actions.

How this helps Java:
- It demonstrates timing control in multithreading.
- It shows how one thread can wait while another thread runs.

Line-by-line explanation:
1. Thread t1 = new Thread(() -> {
   - Creates a new thread.

2. for (int i = 1; i <= 3; i++) {
   - Loop runs three times.

3. System.out.println("Thread running: " + i);
   - Prints the current number.

4. try {
   - Starts exception handling.

5. Thread.sleep(1000);
   - Pauses the thread for 1 second.

6. } catch (InterruptedException e) {
   - Handles interruption exception.

7. e.printStackTrace();
   - Prints error details.

8. }
   - Ends catch block.

9. }
   - Ends loop.

10. });
    - Ends lambda expression.

11. t1.start();
    - Starts the thread.

Comments:
public class SleepExample2 {
    // Program class.
    public static void main(String[] args) {
        // Execution starts here.
        Thread t1 = new Thread(() -> {
            // Creates a new thread.
            for (int i = 1; i <= 3; i++) {
                // Loop runs three times.
                System.out.println("Thread running: " + i);
                // Prints current iteration.
                try {
                    // Tries to pause the thread.
                    Thread.sleep(1000);
                    // Sleeps for 1 second.
                } catch (InterruptedException e) {
                    // Handles exception.
                    e.printStackTrace();
                    // Prints details if interrupted.
                }
            }
        });

        t1.start();
        // Starts the thread.
    }
}

Output example:
Thread running: 1
Thread running: 2
Thread running: 3

Summary:
This program shows how sleep() can pause each iteration of a thread.

================================================================================
8. PROGRAM 3: sleep() WITH TWO THREADS
================================================================================
Headline:
Showing Thread Timing With Multiple Threads

Program:
public class SleepExample3 {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 3; i++) {
                System.out.println("Thread 1: " + i);
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 1; i <= 3; i++) {
                System.out.println("Thread 2: " + i);
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        t1.start();
        t2.start();
    }
}

Why this program is used:
- It shows how two threads can pause and resume at different times.
- It helps learners understand thread coordination and timing.

How this helps Java:
- It teaches how threads can share CPU time with delays.
- It gives a practical example of concurrency.

Line-by-line explanation:
1. Thread t1 = new Thread(() -> {
   - Creates first thread.

2. for (int i = 1; i <= 3; i++) {
   - Loop runs three times.

3. System.out.println("Thread 1: " + i);
   - Prints current value of thread 1.

4. try {
   - Starts exception handling block.

5. Thread.sleep(500);
   - Pauses for 500 milliseconds.

6. } catch (InterruptedException e) {
   - Handles interruption.

7. e.printStackTrace();
   - Prints error details.

8. }
   - Ends block.

9. }
   - Ends loop.

10. });
    - Ends lambda for thread 1.

11. Thread t2 = new Thread(() -> {
    - Creates second thread.

12. for (int i = 1; i <= 3; i++) {
    - Loop runs three times.

13. System.out.println("Thread 2: " + i);
    - Prints current value of thread 2.

14. try {
    - Starts exception handling block.

15. Thread.sleep(500);
    - Pauses for 500 milliseconds.

16. } catch (InterruptedException e) {
    - Handles interruption.

17. e.printStackTrace();
    - Prints error details.

18. }
    - Ends block.

19. }
    - Ends loop.

20. });
    - Ends lambda for thread 2.

21. t1.start();
    - Starts thread 1.

22. t2.start();
    - Starts thread 2.

Comments:
public class SleepExample3 {
    // Program class.
    public static void main(String[] args) {
        // Execution begins here.
        Thread t1 = new Thread(() -> {
            // First thread.
            for (int i = 1; i <= 3; i++) {
                // Repeats three times.
                System.out.println("Thread 1: " + i);
                // Prints thread 1 value.
                try {
                    // Handles possible pause exception.
                    Thread.sleep(500);
                    // Waits for half a second.
                } catch (InterruptedException e) {
                    // Handles interruption.
                    e.printStackTrace();
                    // Prints details.
                }
            }
        });

        Thread t2 = new Thread(() -> {
            // Second thread.
            for (int i = 1; i <= 3; i++) {
                // Repeats three times.
                System.out.println("Thread 2: " + i);
                // Prints thread 2 value.
                try {
                    // Handles possible pause exception.
                    Thread.sleep(500);
                    // Waits for half a second.
                } catch (InterruptedException e) {
                    // Handles interruption.
                    e.printStackTrace();
                    // Prints details.
                }
            }
        });

        t1.start();
        // Starts thread 1.
        t2.start();
        // Starts thread 2.
    }
}

Output example:
Thread 1: 1
Thread 2: 1
Thread 1: 2
Thread 2: 2
Thread 1: 3
Thread 2: 3

Summary:
This program demonstrates how two threads can use sleep() to pause between actions.

================================================================================
9. COMMON MISTAKES WITH sleep()
================================================================================
- Forgetting to handle InterruptedException
- Assuming sleep() guarantees exact timing
- Calling sleep() on the wrong thread
- Using sleep() as a solution for synchronization problems

================================================================================
10. FINAL SUMMARY
================================================================================
The sleep() method is a simple but very important thread method in Java. It pauses
execution for a specified time and allows other threads to run. Although it is not
used for synchronization, it is extremely useful for timing, delays, and scheduling
examples.

================================================================================
11. PROFESSIONAL NOTE FOR REPOSITORY USE
================================================================================
This topic is excellent for a GitHub repository because it includes:
- definition and theory
- multiple practical programs
- code comments
- outputs and summaries
- clear explanation of how timing works in threads

A suggested structure is:
- theory/
- examples/
- outputs/
- notes/
