11 - Daemon Threads in Java

================================================================================
TOPIC OVERVIEW
================================================================================
A daemon thread is a thread that runs in the background and does not prevent the
Java Virtual Machine (JVM) from exiting. These threads are commonly used for tasks
such as garbage collection, monitoring, logging, or background cleanup.

Why this topic is important:
- It explains how background tasks work in Java.
- It helps understand JVM shutdown behavior.
- It is a common interview topic in multithreading.
- It is useful for designing services and utility programs.

================================================================================
1. DEFINITION OF DAEMON THREAD
================================================================================
A daemon thread is a low-priority background thread that supports the main program.
If all non-daemon threads finish, the JVM can terminate even if daemon threads are
still running.

In simple words:
- daemon threads help the program.
- they are not essential for the program's completion.
- they stop automatically when all normal threads are done.

================================================================================
2. DIFFERENCE BETWEEN USER THREAD AND DAEMON THREAD
================================================================================
User thread (non-daemon thread):
- important for program execution
- JVM waits for it to finish before exiting

Daemon thread:
- background thread
- JVM does not wait for it to finish

Example:
- A main program thread is a user thread.
- A background monitor thread may be a daemon thread.

================================================================================
3. HOW TO CREATE A DAEMON THREAD
================================================================================
A thread can be made daemon by calling:

thread.setDaemon(true);

This must be called before starting the thread.

If you call setDaemon(true) after starting the thread, Java throws IllegalThreadStateException.

================================================================================
4. WHY DAEMON THREADS ARE USED
================================================================================
Daemon threads are used for:
- background monitoring
- logging
- auto-saving data
- cleanup tasks
- services that should not block program exit

================================================================================
5. PSEUDOCODE FOR DAEMON THREAD
================================================================================
BEGIN
    CREATE thread
    SET thread as daemon
    START thread

    IF all user threads finish THEN
        JVM exits
        DAEMON thread stops automatically
    ENDIF
END

================================================================================
6. PROGRAM 1: SIMPLE DAEMON THREAD EXAMPLE
================================================================================
Headline:
Creating a Daemon Thread in Java

Program:
public class DaemonExample1 {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            while (true) {
                System.out.println("Daemon thread is running");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        t1.setDaemon(true);
        t1.start();
        System.out.println("Main thread is finishing");
    }
}

Why this program is used:
- It shows how to create a daemon thread.
- It explains why the JVM can exit even when the daemon thread keeps running.

How this helps Java:
- It teaches the concept of background threads.
- It helps understand program shutdown behavior.

Line-by-line explanation:
1. public class DaemonExample1 {
   - Declares the class.

2. public static void main(String[] args) {
   - Entry point of the program.

3. Thread t1 = new Thread(() -> {
   - Creates a thread.

4. while (true) {
   - Creates an infinite loop.

5. System.out.println("Daemon thread is running");
   - Prints status message repeatedly.

6. try {
   - Starts exception handling block.

7. Thread.sleep(1000);
   - Pauses for 1 second.

8. } catch (InterruptedException e) {
   - Handles interruption exception.

9. e.printStackTrace();
   - Prints exception details.

10. }
    - Ends catch block.

11. }
    - Ends loop.

12. });
    - Ends lambda expression.

13. t1.setDaemon(true);
    - Marks thread as daemon.

14. t1.start();
    - Starts the thread.

15. System.out.println("Main thread is finishing");
    - Prints message that main thread is ending.

16. }
    - Ends main.

17. }
    - Ends class.

Comments:
public class DaemonExample1 {
    // Main class.
    public static void main(String[] args) {
        // Program starts here.
        Thread t1 = new Thread(() -> {
            // Creates a new thread.
            while (true) {
                // Infinite loop to keep running.
                System.out.println("Daemon thread is running");
                // Prints a message repeatedly.
                try {
                    // Handles possible sleep interruption.
                    Thread.sleep(1000);
                    // Pauses for 1 second.
                } catch (InterruptedException e) {
                    // Handles interruption.
                    e.printStackTrace();
                    // Prints error details.
                }
            }
        });

        t1.setDaemon(true);
        // Marks the thread as a daemon thread.
        t1.start();
        // Starts the daemon thread.
        System.out.println("Main thread is finishing");
        // Prints message saying the main thread is ending.
    }
}

Output example:
Main thread is finishing
Daemon thread is running
Daemon thread is running
Daemon thread is running

Summary:
This program shows that a daemon thread can continue running in the background while the main thread finishes.

================================================================================
7. PROGRAM 2: CHECKING WHETHER A THREAD IS DAEMON
================================================================================
Headline:
Checking Thread Type Using isDaemon()

Program:
public class DaemonExample2 {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            System.out.println("Thread is running");
        });

        System.out.println("Before setDaemon: " + t1.isDaemon());
        t1.setDaemon(true);
        System.out.println("After setDaemon: " + t1.isDaemon());
    }
}

Why this program is used:
- It shows how to check whether a thread is daemon or non-daemon.
- It explains the role of isDaemon().

How this helps Java:
- It teaches how to verify thread properties during debugging.
- It helps developers understand thread flags clearly.

Line-by-line explanation:
1. Thread t1 = new Thread(() -> {
   - Creates a thread object.

2. System.out.println("Thread is running");
   - Prints a message inside the thread.

3. });
   - Ends lambda expression.

4. System.out.println("Before setDaemon: " + t1.isDaemon());
   - Prints whether the thread is daemon before setting it.

5. t1.setDaemon(true);
   - Marks the thread as a daemon thread.

6. System.out.println("After setDaemon: " + t1.isDaemon());
   - Prints whether the thread is daemon after setting it.

Comments:
public class DaemonExample2 {
    // Program class.
    public static void main(String[] args) {
        // Main method starts execution.
        Thread t1 = new Thread(() -> {
            // Creates a thread.
            System.out.println("Thread is running");
            // Prints a message.
        });

        System.out.println("Before setDaemon: " + t1.isDaemon());
        // Checks if thread is daemon before changing it.
        t1.setDaemon(true);
        // Marks the thread as daemon.
        System.out.println("After setDaemon: " + t1.isDaemon());
        // Checks the daemon status after changing it.
    }
}

Output:
Before setDaemon: false
After setDaemon: true

Summary:
This program shows how to detect and change daemon status using isDaemon() and setDaemon().

================================================================================
8. PROGRAM 3: DAEMON THREAD WITH MAIN THREAD
================================================================================
Headline:
Understanding JVM Exit Behavior With Daemon Threads

Program:
public class DaemonExample3 {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            while (true) {
                System.out.println("Background task running");
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        t1.setDaemon(true);
        t1.start();

        System.out.println("Main thread will end now");
    }
}

Why this program is used:
- It demonstrates that the JVM can shut down when only daemon threads remain.
- It helps explain why daemon threads are suitable for background jobs.

How this helps Java:
- It teaches developers when it is safe to use background tasks.
- It clarifies the lifecycle difference between daemon and user threads.

Line-by-line explanation:
1. public static void main(String[] args) throws InterruptedException {
   - Main method can throw exception.

2. Thread t1 = new Thread(() -> {
   - Creates a background thread.

3. while (true) {
   - Creates infinite loop.

4. System.out.println("Background task running");
   - Prints output repeatedly.

5. try {
   - Handles possible interruption.

6. Thread.sleep(500);
   - Pauses for 0.5 seconds.

7. } catch (InterruptedException e) {
   - Handles sleep interruption.

8. e.printStackTrace();
   - Prints exception details.

9. }
   - Ends catch block.

10. }
    - Ends loop.

11. });
    - Ends lambda expression.

12. t1.setDaemon(true);
    - Makes the thread a daemon.

13. t1.start();
    - Starts the daemon thread.

14. System.out.println("Main thread will end now");
    - Prints message before main thread finishes.

Comments:
public class DaemonExample3 {
    // Program class.
    public static void main(String[] args) throws InterruptedException {
        // Main method may throw an exception.
        Thread t1 = new Thread(() -> {
            // Creates background thread.
            while (true) {
                // Loops forever.
                System.out.println("Background task running");
                // Prints status message.
                try {
                    // Handles sleep exception.
                    Thread.sleep(500);
                    // Pauses for half a second.
                } catch (InterruptedException e) {
                    // Handles exception.
                    e.printStackTrace();
                    // Prints error details.
                }
            }
        });

        t1.setDaemon(true);
        // Marks thread as daemon.
        t1.start();
        // Starts the thread.
        System.out.println("Main thread will end now");
        // Main thread is about to finish.
    }
}

Output example:
Main thread will end now
Background task running
Background task running
Background task running

Summary:
This example shows that once the main thread finishes, the daemon thread is stopped automatically by the JVM.

================================================================================
9. IMPORTANT RULES FOR DAEMON THREADS
================================================================================
- setDaemon(true) must be called before start().
- Daemon threads are mainly for background support.
- They should not be used for important tasks like saving crucial data.
- You should not rely on them for finishing critical work.

================================================================================
10. FINAL SUMMARY
================================================================================
Daemon threads are background threads that allow the JVM to exit when all non-daemon
threads have finished. They are useful for tasks like monitoring, logging, and cleanup.
However, because they are not guaranteed to complete, they should not be used for critical
operations that must always finish.

================================================================================
11. PROFESSIONAL NOTE FOR REPOSITORY USE
================================================================================
This topic is ideal for a GitHub repository because it includes:
- definitions and theory
- examples with comments
- outputs and summaries
- practical concepts about JVM behavior

A good layout for this topic is:
- theory/
- examples/
- outputs/
- notes/
