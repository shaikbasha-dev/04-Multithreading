12 - Synchronization in Java

================================================================================
TOPIC OVERVIEW
================================================================================
Synchronization in Java is used to control access to shared resources when multiple
threads are running at the same time. It helps prevent problems such as inconsistent
results, race conditions, and data corruption.

Why this topic is important:
- It is one of the most important concepts in multithreading.
- It helps protect shared data.
- It is essential for writing correct concurrent programs.
- It is frequently asked in technical interviews and practical coding tasks.

================================================================================
1. DEFINITION OF SYNCHRONIZATION
================================================================================
Synchronization means allowing only one thread to access a shared resource at a time.
It ensures that the critical section of code is executed safely.

A critical section is a block of code that accesses shared data or resources.

================================================================================
2. WHY SYNCHRONIZATION IS NEEDED
================================================================================
Without synchronization, multiple threads may read or modify the same variable at the
same time, causing incorrect results.

This can lead to:
- race conditions
- inconsistent outputs
- corrupted data
- unpredictable behavior

================================================================================
3. WHAT IS A RACE CONDITION?
================================================================================
A race condition happens when two or more threads access shared data at the same time
and the final result depends on the timing of execution.

Example:
If two threads both increase a counter from 5 to 6 at the same moment, the final result
may be wrong if the update is not protected.

================================================================================
4. TYPES OF SYNCHRONIZATION IN JAVA
================================================================================
1. Synchronized method
   - A method can be made synchronized so that only one thread runs it at a time.

2. Synchronized block
   - A block of code can be synchronized to lock only a specific part.

3. Static synchronization
   - Used when shared data belongs to the class rather than an object.

================================================================================
5. KEY WORD: synchronized
================================================================================
The synchronized keyword is used to make a method or block thread-safe.

Syntax:
public synchronized void methodName() {
    // critical section
}

Or:
synchronized (object) {
    // critical section
}

================================================================================
6. PSEUDOCODE FOR SYNCHRONIZATION
================================================================================
BEGIN
    LOCK shared resource
    PERFORM read/update operation
    UNLOCK shared resource
END

This ensures that only one thread can access the resource at a time.

================================================================================
7. PROGRAM 1: WITHOUT SYNCHRONIZATION
================================================================================
Headline:
Showing the Problem of Shared Data Without Synchronization

Program:
class Counter {
    int count = 0;

    void increment() {
        count++;
    }
}

public class SyncExample1 {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final count: " + counter.count);
    }
}

Why this program is used:
- It shows what happens when multiple threads update the same variable without synchronization.
- It helps explain the concept of race conditions.

How this helps Java:
- It teaches why thread-safe programming is important.
- It demonstrates that shared data needs protection.

Line-by-line explanation:
1. class Counter {
   - Declares a class that stores a shared counter.

2. int count = 0;
   - Creates a shared variable.

3. void increment() {
   - Defines a method that increases the count.

4. count++;
   - Increases the value of count by one.

5. }
   - Ends increment method.

6. }
   - Ends class.

7. public class SyncExample1 {
   - Declares main class.

8. public static void main(String[] args) throws InterruptedException {
   - Main method may throw InterruptedException.

9. Counter counter = new Counter();
   - Creates a shared Counter object.

10. Thread t1 = new Thread(() -> {
    - Creates first thread.

11. for (int i = 0; i < 1000; i++) {
    - Loop runs 1000 times.

12. counter.increment();
    - Calls increment method.

13. }
    - Ends loop.

14. });
    - Ends thread code.

15. Thread t2 = new Thread(() -> {
    - Creates second thread.

16. for (int i = 0; i < 1000; i++) {
    - Loop runs 1000 times.

17. counter.increment();
    - Calls increment method.

18. }
    - Ends loop.

19. });
    - Ends thread code.

20. t1.start();
    - Starts thread 1.

21. t2.start();
    - Starts thread 2.

22. t1.join();
    - Waits for thread 1 to finish.

23. t2.join();
    - Waits for thread 2 to finish.

24. System.out.println("Final count: " + counter.count);
    - Prints final count.

25. }
    - Ends main.

26. }
    - Ends class.

Comments:
class Counter {
    // Class that holds a shared variable.
    int count = 0;
    // Shared counter value.

    void increment() {
        // Method to increase the counter.
        count++;
        // Increases the value by 1.
    }
}

public class SyncExample1 {
    // Main class.
    public static void main(String[] args) throws InterruptedException {
        // Main method may throw an exception.
        Counter counter = new Counter();
        // Creates a shared object.

        Thread t1 = new Thread(() -> {
            // First worker thread.
            for (int i = 0; i < 1000; i++) {
                // Repeats 1000 times.
                counter.increment();
                // Increases the shared counter.
            }
        });

        Thread t2 = new Thread(() -> {
            // Second worker thread.
            for (int i = 0; i < 1000; i++) {
                // Repeats 1000 times.
                counter.increment();
                // Increases the shared counter.
            }
        });

        t1.start();
        // Starts thread 1.
        t2.start();
        // Starts thread 2.
        t1.join();
        // Waits for thread 1 to finish.
        t2.join();
        // Waits for thread 2 to finish.

        System.out.println("Final count: " + counter.count);
        // Prints the final count.
    }
}

Output example:
Final count: 1982

Summary:
This example shows that without synchronization, the final result may not be correct.

================================================================================
8. PROGRAM 2: WITH SYNCHRONIZED METHOD
================================================================================
Headline:
Fixing Shared Data Problems Using synchronized Method

Program:
class Counter {
    int count = 0;

    synchronized void increment() {
        count++;
    }
}

public class SyncExample2 {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final count: " + counter.count);
    }
}

Why this program is used:
- It shows how synchronization fixes the issue.
- It ensures that only one thread increments the counter at a time.

How this helps Java:
- It teaches how to protect shared data.
- It demonstrates the role of synchronized methods in thread safety.

Line-by-line explanation:
1. synchronized void increment() {
   - Makes the increment method synchronized.

2. count++;
   - Increases the shared counter safely.

3. }
   - Ends the synchronized method.

Comments:
class Counter {
    // Holds shared data.
    int count = 0;
    // Shared counter.

    synchronized void increment() {
        // Only one thread can enter this method at a time.
        count++;
        // Updates the counter safely.
    }
}

public class SyncExample2 {
    // Main class.
    public static void main(String[] args) throws InterruptedException {
        // Main method may throw exception.
        Counter counter = new Counter();
        // Shared counter object.

        Thread t1 = new Thread(() -> {
            // First thread.
            for (int i = 0; i < 1000; i++) {
                // Repeats 1000 times.
                counter.increment();
                // Safely increments count.
            }
        });

        Thread t2 = new Thread(() -> {
            // Second thread.
            for (int i = 0; i < 1000; i++) {
                // Repeats 1000 times.
                counter.increment();
                // Safely increments count.
            }
        });

        t1.start();
        // Starts thread 1.
        t2.start();
        // Starts thread 2.
        t1.join();
        // Waits for thread 1.
        t2.join();
        // Waits for thread 2.

        System.out.println("Final count: " + counter.count);
        // Prints correct final result.
    }
}

Output:
Final count: 2000

Summary:
This example shows that synchronization ensures the counter is updated correctly.

================================================================================
9. PROGRAM 3: USING SYNCHRONIZED BLOCK
================================================================================
Headline:
Protecting a Specific Code Region with synchronized Block

Program:
class SharedResource {
    int value = 0;

    void update() {
        synchronized (this) {
            value++;
        }
    }
}

public class SyncExample3 {
    public static void main(String[] args) throws InterruptedException {
        SharedResource resource = new SharedResource();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                resource.update();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                resource.update();
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final value: " + resource.value);
    }
}

Why this program is used:
- It demonstrates synchronization at block level.
- It shows that only a part of the code needs protection.

How this helps Java:
- It teaches that synchronization can be applied precisely.
- It improves efficiency when only a small section of code is critical.

Line-by-line explanation:
1. synchronized (this) {
   - Locks the current object for the block.

2. value++;
   - Updates the shared value safely.

3. }
   - Unlocks the object.

Comments:
class SharedResource {
    // Class containing shared data.
    int value = 0;
    // Shared variable.

    void update() {
        // Method that modifies shared data.
        synchronized (this) {
            // Only one thread can enter this block at a time.
            value++;
            // Increments the shared variable safely.
        }
    }
}

public class SyncExample3 {
    // Main class.
    public static void main(String[] args) throws InterruptedException {
        // Main method may throw exception.
        SharedResource resource = new SharedResource();
        // Creates shared resource object.

        Thread t1 = new Thread(() -> {
            // First thread.
            for (int i = 0; i < 1000; i++) {
                // Repeats 1000 times.
                resource.update();
                // Calls synchronized update.
            }
        });

        Thread t2 = new Thread(() -> {
            // Second thread.
            for (int i = 0; i < 1000; i++) {
                // Repeats 1000 times.
                resource.update();
                // Calls synchronized update.
            }
        });

        t1.start();
        // Starts first thread.
        t2.start();
        // Starts second thread.
        t1.join();
        // Waits for first thread.
        t2.join();
        // Waits for second thread.

        System.out.println("Final value: " + resource.value);
        // Prints final result.
    }
}

Output:
Final value: 2000

Summary:
This example shows how a synchronized block protects a specific portion of code.

================================================================================
10. IMPORTANT NOTE ABOUT SYNCHRONIZATION
================================================================================
Synchronization is powerful, but it should be used carefully.
Too much synchronization can reduce performance and may even cause deadlock if not handled correctly.

================================================================================
11. FINAL SUMMARY
================================================================================
Synchronization in Java is used to make shared resources safe for multiple threads.
It prevents race conditions by allowing only one thread to access a critical section
at a time. Using synchronized methods or synchronized blocks is essential for writing
correct thread-safe programs.

================================================================================
12. PROFESSIONAL NOTE FOR REPOSITORY USE
================================================================================
This topic is excellent for a GitHub repository because it includes:
- theory of synchronization
- examples of race conditions and fixes
- clear code comments
- outputs and summary sections
- practical explanation of thread safety

A good folder structure could be:
- theory/
- examples/
- outputs/
- notes/
