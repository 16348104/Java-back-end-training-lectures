# Multithreading

> Java is a multi-threaded programming language

1. Process and thread
    - A process is an execution of a program and a thread is a single execution of work within the process. 
    - A process can contain multiple threads. 
    - A thread is also known as a lightweight process.

2. Thread lifecycle
    - Runnable
    - Running
    - Waiting
    - Sleeping
    - Blocked on I/O
    - Blocked on synchronization
    - Dead
    
3. Implementation
    - Extend `Thread` class
        
        ```java
        public class SubThread extends Thread {
            @Override
            public void run() {
                System.out.println("SubThread...");
            }
        
            public static void main(String[] args) {
                new SubThread().start();
            }
        }
        ```
        
    - Implement `Runnable` interface
        ```java
        public class RunnableImpl implements Runnable {
            @Override
            public void run() {
                System.out.println("RunnableImpl...");
            }
        
            public static void main(String[] args) {
                new Thread(new RunnableImpl()).start();
            }
        }
        ```

4. Multithreading
    
    ```java
    public class Multithreading implements Runnable {
    
        @Override
        public void run() {
            try {
                System.out.println("runnable thread: " + Thread.currentThread().getName());
                Thread.sleep(1000 * 3);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    
        public static void main(String[] args) {
            Thread thread1 = new Thread(new Multithreading());
            thread1.setName("thread1");
            Thread thread2 = new Thread(new Multithreading());
            thread2.setName("thread2");
            SubThread thread3 = new SubThread();
            thread3.setName("thread3");
    
            thread1.start();
            thread2.start();
            try {
                thread2.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            thread3.start();
        }
    }
    ```

5. Thread priority
    - `MIN_PRIORITY` 1
    - `MAX_PRIORITY` 10
    - `NORMAL_PRIORITY` 5
    
    ```java
    public class ThreadPriority implements Runnable {
        @Override
        public void run() {
            System.out.println("running thread: " + Thread.currentThread().getName());
            System.out.println("thread priority: " + Thread.currentThread().getPriority());
        }
    
        public static void main(String[] args) {
            Thread thread1 = new Thread(new ThreadPriority());
            Thread thread2 = new Thread(new ThreadPriority());
            Thread thread3 = new Thread(new ThreadPriority());
    
            thread1.setName("thread1");
            thread2.setName("thread2");
            thread3.setName("thread3");
    
            thread1.setPriority(Thread.MIN_PRIORITY);
            thread2.setPriority(Thread.MAX_PRIORITY);
            thread3.setPriority(Thread.NORM_PRIORITY);
    
            thread1.start();
            thread2.start();
            thread3.start();
        }
    }
    ```
    
6. Synchronization
    - synchronization method
    - synchronization block
    
    ```java
    public class Synchronization {
        public static void main(String[] args) {
            Output output = new Output();
            Library library = new Library(output);
            University university = new University(output);
    
            library.start();
            university.start();
        }
    }
    
    class Output {
        public synchronized void print(String s) {
            System.out.println(s);
            try {
                Thread.sleep(1000*5);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    
        public void scan(String s) {
            synchronized (s) {
                try {
                    s.wait(1000*5);
                    System.out.println("scan: " + s);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    
    class Library extends Thread {
    
        private Output output;
    
        public Library(Output output) {
            this.output = output;
        }
    
        @Override
        public void run() {
            output.print("library print...");
    //        output.scan("library print...");
        }
    }
    
    class University extends Thread {
        private Output output;
    
        public University(Output output) {
            this.output = output;
        }
    
        @Override
        public void run() {
            output.print("University print...");
    //        output.scan("University print...");
        }
    }
    ```
    
7. Thread safe
    - `Vector`
    - `Stack`
    - `Hashtable`