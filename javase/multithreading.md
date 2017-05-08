# 补3. 多线程 `Multithreading`

> Java is a multi-threaded programming language

1. Process and thread
    - A process is an execution of a program and a thread is a single execution of work within the process. 
    - A process can contain multiple threads. 
    - A thread is also known as a lightweight process.

2. Thread lifecycle
    - 新建 `new`
    - 就绪 `Runnable`
    - 运行 `Running`
    - 阻塞 `Blocked`
        - 等待阻塞 `Waiting`
        - 同步阻塞 `Blocked on synchronization`
        - 其他阻塞
            - I/O
            - Sleeping
            - join
    -  死亡   `Dead`
    
    <img src="../image/javase/thread_states.png">
    
3. Implementation
    - Extend `Thread` class
        
        ```java
        public class MT1 extends Thread {
        
            public static void main(String[] args) {
                MT1 mt1 = new MT1();
                mt1.start();
                System.out.println("test...");
            }
        
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    System.out.println(i);
                }
            }
        }
        ```
        
    - Implement `Runnable` interface
    
        ```java
        public class MT2 implements Runnable {
            public static void main(String[] args) {
                MT2 mt2 = new MT2();
                Thread thread = new Thread(mt2);
                thread.start();
                System.out.println("test...");
            }
        
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    System.out.println(i);
                }
            }
        }
        ```
        
4. join

    ```java
    public class MT4 implements Runnable {
    
        public static void main(String[] args) {
    
            Thread thread = new Thread(new MT4());
            thread.setName("thread");
            thread.start();
    
            try {
                thread.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
    
            System.out.println("test...");
        }
    
        @Override
        public void run() {
            for (int i = 0; i < 3; i++) {
                System.out.println(Thread.currentThread().getName() + " is running...");
                try {
                    Thread.sleep(1000 * 3);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    ```
    
    ```java
    public class MT5 implements Runnable {
    
        public static void main(String[] args) {
    
            Thread thread1 = new Thread(new MT5());
            thread1.setName("thread 1");
            Thread thread2 = new Thread(new MT5());
            thread2.setName("thread 2");
            Thread thread3 = new Thread(new MT5());
            thread3.setName("thread 3");
    
            thread1.start();
            thread2.start();
    
            try {
                thread2.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
    
            thread3.start();
    
            System.out.println("test...");
        }
    
        @Override
        public void run() {
            for (int i = 0; i < 3; i++) {
                System.out.println(Thread.currentThread().getName() + " is running...");
                try {
                    Thread.sleep(1000 * 1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    ```
    
5. yield `[jiːld] `    

    ```java
    public class MT6 implements Runnable {
    
        public static void main(String[] args) {
            Thread thread1 = new Thread(new MT6());
            thread1.setName("thread 1");
            Thread thread2 = new Thread(new MT6());
            thread2.setName("thread 2");
    
            thread1.start();
            thread2.start();
    
            System.out.println("test...");
        }
    
        @Override
        public void run() {
            for (int i = 0; i < 100; i++) {
                System.out.println(i + ": " + Thread.currentThread().getName() + " is running...");
                if (i % 10 == 0) {
                    Thread.yield();
                }
            }
        }
    }
    ```

6. Thread priority
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
    
7. Synchronization
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
    
8. Thread safe
    - `Vector`
    - `Stack`
    - `Hashtable`