# 补3. 多线程 `Multithreading`

> Java is a multi-threaded programming language

1. Process and thread
    - A process is an execution of a program and a thread is a single execution of work within the process. 
    - A process can contain multiple threads. 
    - A thread is also known as a lightweight process.

2. Thread lifecycle
    - 新建 `New`
    - 就绪 `Runnable`
    - 运行 `Running`
    - 阻塞 `Blocked`
        - 等待阻塞 `Waiting`
        - 同步阻塞 `Blocked on synchronization`
        - 其他阻塞
            - I/O
            - Sleep
            - Join
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
    
    - `synchronized` 作用域
        - 对象 / 实例 范围
          
          > 一个线程只能访问一个对象的 synchronized 方法，但其他线程可以访问另一个对象的同一方法
          
        - 类范围
              
          > 一个线程只能访问一个类的一个 synchronized static 方法，对这个类的所有对象都适用
    
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
 
8. `wait` `notify` `notifyAll`
    
    >  来自 `Object` 类，线程间通讯的方式

    - `wait`
        
        ```java
        public final void wait() throws InterruptedException, IllegalMonitorStateException
        ```
    
        - 当前线程阻塞
        - 等待其他线程调用 `notify` 或 `notifyAll`
        - 调用后，线程释放锁
        - 被唤醒后，重新竞争锁
        - 调用 `wait` 时，线程必须获得对象级别锁，即，在同步方法或同步块中
        - 如果调用时没有锁，抛 `IllegalMonitorStateException` 运行时异常
        
    - `notify`
    
        ```java
        public final native void notify() throws IllegalMonitorStateException
        ```
        
        - 唤醒正在 wait 的线程，如有多个，挑选一个
        - 通知后，当前线程不会马上释放锁，wait 线程不会马上获得锁，需要等待退出同步区
        - 被唤醒的线程获得锁并执行完成，如果没有继续 notify，其他 wait 线程继续阻塞，等待被唤醒
        - 调用 `notify` 时，线程必须获得对象级别锁，即，在同步方法或同步块中
        - 如果调用时没有锁，抛 `IllegalMonitorStateException` 运行时异常
        
    - `notifyAll`
        
        ```java
        public final native void notifyAll() throws IllegalMonitorStateException
        ```
        - 唤醒全部 wait 的线程
        - 当前线程退出同步区时，所有被唤醒线程竞争锁
        - 得到锁的线程执行完成同步区，其他线程继续竞争锁，知道全部执行完成
        - 调用 `wait` 时，线程必须获得对象级别锁，即，在同步方法或同步块中
        - 如果调用时没有锁，抛 `IllegalMonitorStateException` 运行时异常
        
9. 生产者与消费者问题
    
   > Producer-consumer problem
   
   > 保证生产者不会在缓冲区满时加入数据，消费者也不会在缓冲区中空时消耗数据。
   
   ```
                                 +------------------+
                                 |                  |
                                 |                  |
                                 |                  |
                                 |                  |
                                 |                  |
                                 |                  |
                                 |                  |
   +-------------------+         |                  |         +------------------+
   |                   |         |                  |         |                  |
   |                   |         |                  |         |                  |
   |     Producer      | +-----> |      Buffer      | +-----> |     Consumer     |
   |                   |         |                  |         |                  |
   |                   |         |                  |         |                  |
   |                   |         |                  |         |                  |
   +-------------------+         |                  |         +------------------+
                                 |                  |
                                 |                  |
                                 |                  |
                                 |                  |
                                 |                  |
                                 |                  |
                                 +------------------+

   ```