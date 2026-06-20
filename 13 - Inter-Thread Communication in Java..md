13 - Inter-Thread Communication in Java

================================================================================
TOPIC OVERVIEW
================================================================================
Inter-thread communication is the process by which one thread communicates with
another thread so they can coordinate their work. In Java, this is mainly achieved
using methods such as wait(), notify(), and notifyAll().

Why this topic is important:
- It explains how threads can cooperate.
- It helps avoid busy waiting.
- It is essential for solving producer-consumer problems.
- It is a key concept in advanced multithreading.

================================================================================
1. DEFINITION OF INTER-THREAD COMMUNICATION
================================================================================
Inter-thread communication means allowing threads to exchange information and
coordinate their execution.

Instead of running independently without awareness of each other, threads can:
- signal each other
- wait for a condition to become true
- resume execution after another thread completes a task

================================================================================
2. WHY COMMUNICATION BETWEEN THREADS IS NEEDED
================================================================================
Threads often share resources. For example:
- one thread produces data
- another thread consumes data

If the consumer runs before the producer has prepared data, the program may behave
incorrectly. Inter-thread communication solves this problem.

================================================================================
3. METHODS USED FOR COMMUNICATION
================================================================================
The main methods are:
- wait()
  - makes the current thread wait until another thread notifies it
- notify()
  - wakes up one waiting thread
- notifyAll()
  - wakes up all waiting threads

These methods are declared in the Object class and must be called inside synchronized code.

================================================================================
4. IMPORTANT RULES
================================================================================
- wait(), notify(), and notifyAll() are called only from inside synchronized block or method.
- A thread releases the lock when it calls wait().
- After notify(), the waiting thread becomes ready, but it does not run immediately.
- notifyAll() is safer when multiple threads may be waiting.

================================================================================
5. PSEUDOCODE FOR INTER-THREAD COMMUNICATION
================================================================================
BEGIN
    THREAD 1:
        LOCK shared object
        CHECK condition
        IF condition is false THEN
            CALL wait()
        ENDIF
        PERFORM action
        CALL notify()
        UNLOCK

    THREAD 2:
        LOCK shared object
        CHANGE condition
        CALL notify()
        UNLOCK
END

================================================================================
6. PROGRAM 1: SIMPLE wait() AND notify() EXAMPLE
================================================================================
Headline:
Using wait() and notify() to Coordinate Threads

Program:
class SharedResource {
    private int value = 0;
    private boolean flag = false;

    synchronized void produce() {
        while (flag) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        value = 10;
        flag = true;
        System.out.println("Producer produced: " + value);
        notify();
    }

    synchronized void consume() {
        while (!flag) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        System.out.println("Consumer consumed: " + value);
        flag = false;
        notify();
    }
}

public class InterThreadExample1 {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Thread producer = new Thread(() -> {
            for (int i = 0; i < 2; i++) {
                resource.produce();
            }
        });

        Thread consumer = new Thread(() -> {
            for (int i = 0; i < 2; i++) {
                resource.consume();
            }
        });

        producer.start();
        consumer.start();
    }
}

Why this program is used:
- It demonstrates how one thread can wait for another thread to finish a task.
- It explains the producer-consumer pattern.

How this helps Java:
- It teaches how threads can communicate safely.
- It prevents busy waiting by using wait() and notify().

Line-by-line explanation:
1. class SharedResource {
   - Declares a class that stores shared data.

2. private int value = 0;
   - Stores data produced by one thread.

3. private boolean flag = false;
   - Tracks whether data is available.

4. synchronized void produce() {
   - Defines synchronized producer method.

5. while (flag) {
   - Loops while the data is still available.

6. try {
   - Begins exception handling block.

7. wait();
   - Makes the producer wait until the consumer is ready.

8. } catch (InterruptedException e) {
   - Handles interruption.

9. e.printStackTrace();
   - Prints exception details.

10. }
    - Ends catch block.

11. }
    - Ends while loop.

12. value = 10;
    - Sets data value.

13. flag = true;
    - Marks that the data is ready.

14. System.out.println("Producer produced: " + value);
    - Prints produced value.

15. notify();
    - Notifies waiting consumer.

16. }
    - Ends produce method.

17. synchronized void consume() {
    - Defines synchronized consumer method.

18. while (!flag) {
    - Loops while the data is not ready.

19. try {
    - Starts exception handling block.

20. wait();
    - Makes consumer wait until producer signals.

21. } catch (InterruptedException e) {
    - Handles exception.

22. e.printStackTrace();
    - Prints exception details.

23. }
    - Ends catch block.

24. }
    - Ends while loop.

25. System.out.println("Consumer consumed: " + value);
    - Prints consumed value.

26. flag = false;
    - Marks that data has been consumed.

27. notify();
    - Notifies producer that consumer is ready again.

28. }
    - Ends consume method.

29. }
    - Ends class.

30. public class InterThreadExample1 {
    - Main class.

31. public static void main(String[] args) {
    - Main method.

32. SharedResource resource = new SharedResource();
    - Creates shared object.

33. Thread producer = new Thread(() -> {
    - Creates producer thread.

34. for (int i = 0; i < 2; i++) {
    - Runs twice.

35. resource.produce();
    - Calls producer method.

36. }
    - Ends loop.

37. });
    - Ends lambda.

38. Thread consumer = new Thread(() -> {
    - Creates consumer thread.

39. for (int i = 0; i < 2; i++) {
    - Runs twice.

40. resource.consume();
    - Calls consumer method.

41. }
    - Ends loop.

42. });
    - Ends lambda.

43. producer.start();
    - Starts producer thread.

44. consumer.start();
    - Starts consumer thread.

45. }
    - Ends main.

46. }
    - Ends class.

Comments:
class SharedResource {
    // Shared object used by producer and consumer.
    private int value = 0;
    // Shared data.
    private boolean flag = false;
    // Indicates whether data is ready.

    synchronized void produce() {
        // Producer method is synchronized.
        while (flag) {
            // Wait while data is already available.
            try {
                wait();
                // Makes producer wait.
            } catch (InterruptedException e) {
                // Handles interruption.
                e.printStackTrace();
                // Prints error details.
            }
        }

        value = 10;
        // Sets value for production.
        flag = true;
        // Marks that data is ready.
        System.out.println("Producer produced: " + value);
        // Prints produced data.
        notify();
        // Wakes up waiting consumer.
    }

    synchronized void consume() {
        // Consumer method is synchronized.
        while (!flag) {
            // Wait while data is not ready.
            try {
                wait();
                // Makes consumer wait.
            } catch (InterruptedException e) {
                // Handles interruption.
                e.printStackTrace();
                // Prints error details.
            }
        }

        System.out.println("Consumer consumed: " + value);
        // Prints consumed data.
        flag = false;
        // Marks data as consumed.
        notify();
        // Wakes up waiting producer.
    }
}

public class InterThreadExample1 {
    // Main class.
    public static void main(String[] args) {
        // Program starts here.
        SharedResource resource = new SharedResource();
        // Creates shared resource object.

        Thread producer = new Thread(() -> {
            // Creates producer thread.
            for (int i = 0; i < 2; i++) {
                // Runs twice.
                resource.produce();
                // Produces data.
            }
        });

        Thread consumer = new Thread(() -> {
            // Creates consumer thread.
            for (int i = 0; i < 2; i++) {
                // Runs twice.
                resource.consume();
                // Consumes data.
            }
        });

        producer.start();
        // Starts producer thread.
        consumer.start();
        // Starts consumer thread.
    }
}

Output example:
Producer produced: 10
Consumer consumed: 10
Producer produced: 10
Consumer consumed: 10

Summary:
This program demonstrates how wait() and notify() enable coordination between two threads.

================================================================================
7. PROGRAM 2: USING notifyAll()
================================================================================
Headline:
Waking Up All Waiting Threads Using notifyAll()

Program:
class MessageBox {
    private String message;
    private boolean available = false;

    synchronized void put(String message) {
        while (available) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        this.message = message;
        available = true;
        System.out.println("Produced: " + message);
        notifyAll();
    }

    synchronized String take() {
        while (!available) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        String msg = message;
        available = false;
        System.out.println("Consumed: " + msg);
        notifyAll();
        return msg;
    }
}

public class InterThreadExample2 {
    public static void main(String[] args) {
        MessageBox box = new MessageBox();

        Thread producer = new Thread(() -> {
            for (int i = 1; i <= 3; i++) {
                box.put("Message " + i);
            }
        });

        Thread consumer = new Thread(() -> {
            for (int i = 1; i <= 3; i++) {
                box.take();
            }
        });

        producer.start();
        consumer.start();
    }
}

Why this program is used:
- It shows how notifyAll() can wake all waiting threads.
- It is useful when multiple threads may be waiting for a shared resource.

How this helps Java:
- It teaches a safer way to signal multiple waiting threads.
- It is useful in larger applications where multiple consumers may exist.

Line-by-line explanation:
1. synchronized void put(String message) {
   - Producer method is synchronized.

2. while (available) {
   - Wait if the resource is already filled.

3. wait();
   - Makes the current thread wait.

4. this.message = message;
   - Stores the message.

5. available = true;
   - Marks the message as available.

6. notifyAll();
   - Wakes all waiting threads.

7. synchronized String take() {
   - Consumer method is synchronized.

8. while (!available) {
   - Wait if no message is available.

9. String msg = message;
   - Stores message locally.

10. available = false;
    - Marks that message has been consumed.

11. notifyAll();
    - Wakes waiting producer and consumer threads.

Comments:
class MessageBox {
    // Shared box for messages.
    private String message;
    // Stores current message.
    private boolean available = false;
    // Shows if message is ready.

    synchronized void put(String message) {
        // Producer method.
        while (available) {
            // Wait until box is empty.
            try {
                wait();
                // Wait for consumer to read.
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        this.message = message;
        // Store the new message.
        available = true;
        // Mark message as ready.
        System.out.println("Produced: " + message);
        // Print produced message.
        notifyAll();
        // Wake all waiting threads.
    }

    synchronized String take() {
        // Consumer method.
        while (!available) {
            // Wait until message exists.
            try {
                wait();
                // Wait for producer to send data.
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        String msg = message;
        // Save the message.
        available = false;
        // Mark message as consumed.
        System.out.println("Consumed: " + msg);
        // Print consumed message.
        notifyAll();
        // Wake all waiting threads.
        return msg;
    }
}

public class InterThreadExample2 {
    // Main class.
    public static void main(String[] args) {
        // Program starts here.
        MessageBox box = new MessageBox();
        // Creates shared message box.

        Thread producer = new Thread(() -> {
            // Producer thread.
            for (int i = 1; i <= 3; i++) {
                // Runs three times.
                box.put("Message " + i);
                // Produces message.
            }
        });

        Thread consumer = new Thread(() -> {
            // Consumer thread.
            for (int i = 1; i <= 3; i++) {
                // Runs three times.
                box.take();
                // Consumes message.
            }
        });

        producer.start();
        // Starts producer.
        consumer.start();
        // Starts consumer.
    }
}

Output example:
Produced: Message 1
Consumed: Message 1
Produced: Message 2
Consumed: Message 2
Produced: Message 3
Consumed: Message 3

Summary:
This example shows how notifyAll() wakes all waiting threads so coordination remains safe.

================================================================================
8. COMMON PROBLEMS IN INTER-THREAD COMMUNICATION
================================================================================
- Using wait() without synchronization
- Forgetting to use while instead of if
- Using notify() when notifyAll() is safer
- Not checking conditions carefully
- Causing deadlock by improper locking

================================================================================
9. FINAL SUMMARY
================================================================================
Inter-thread communication allows threads to cooperate by sharing signals and
waiting for conditions. It is mainly done using wait(), notify(), and notifyAll().
These methods help solve real-world problems such as producer-consumer scenarios and
make multithreaded programs more reliable.

================================================================================
10. PROFESSIONAL NOTE FOR REPOSITORY USE
================================================================================
This topic is excellent for a GitHub repository because it includes:
- clear theory of communication between threads
- important rules and examples
- commented programs
- output sections
- practical producer-consumer patterns

A good structure is:
- theory/
- examples/
- outputs/
- notes/
