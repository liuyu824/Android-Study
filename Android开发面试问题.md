# **Android开发面试问题**

### Java

##### equals和==的区别

对于==，基本数据类型，比较的是值是否相等，引用数据类型，比较的是对象地址是否相等。对于equal，默认对象地址。String，重写了方法，比较的是值是否相同。



- 

##### HashMap



##### 



##### 如何解决同一个变量同时被多个线程改动的情况



##### 



##### 几种新建线程的方式

1. 继承Thread类，重写run()方法，编写线程执行的代码。创建子类对象，调用start()方法。

   ```java
   public class MyThread extends Thread {
       public void run(){
           // 线程执行的代码
       }
   }
    
   public class Main {
       public static void main(String[] args){
           MyThread myThread = new MyThread();
           myThread.start();
       }
   }
   ```

2. 实现Runnable接口，充血runnable里面的run()方法。在主方法里创建Runnable和Thread类的实例，并将runnable实例作为Thread参数，调用start()方法。

   ```java
   class MyRunnable implements Runnable {
       @Override
       public void run() {
           System.out.println("实现Runnable接口，重写run方法");
       }
   }
    
   public class Main {
       public static void main(String[] args) {
           MyRunnable myRunnable = new MyRunnable();
           Thread thread = new Thread(myRunnable);
           thread.start();
       }
   }
   ```

3. 使用匿名内部类创建线程

   ```java
   Thread thread = new Thread(){
     @Override
     public void run() {
       super.run();
       Log.d(TAG, "run: 新建线程1");
     }
   };
   thread.start();
   ```

4. 使用匿名内部类，实现Runnable接口

   ```java
   Runnable runnable = new Runnable() {
     @Override
     public void run() {
       Log.d(TAG, "run: 新建线程2");
     }
   };
   Thread thread1 = new Thread(runnable);
   thread1.start();
   ```

5. 使用 Lambda 表达式创建线程（需要 Java 8 及以上版本）：

   ```java
   public class Main {
       public static void main(String[] args) {
           Thread thread = new Thread(() -> {
              System.out.println("使用lambda表示创建线程");
           });
           thread.start();
       }
   }
   ```

6. 

7. 使用线程池创建线程

   线程池的单纯使用很简单，使用submit方法，把任务提交到线程池中即可，线程池中会有线程来完成这些任务；

   ```java
   import java.util.concurrent.ExecutorService;
   import java.util.concurrent.Executors;
    
   public class Pool {
     public static void main(String[] args) {
       ExecutorService pool = Executors.newCachedThreadPool();
       pool.submit(new Runnable() {
         @Override
         public void run() {
           //执行业务逻辑
           for(int i = 1; i <= 100; i++) {
             System.out.println("线程:"+Thread.currentThread().getName() + "执行了任务" + i + "~");
           }
         }
       });
       pool.submit(new Runnable() {
         @Override
         public void run() {
           //执行业务逻辑
           for(int i = 101; i <= 200; i++) {
             System.out.println("线程:" + Thread.currentThread().getName() + "执行了任务" + i + "~");
           }
         }
       });
       pool.submit(new Runnable() {
         @Override
         public void run() {
           //执行业务逻辑
           for(int i = 201; i <= 300; i++) {
             System.out.println("线程:" + Thread.currentThread().getName() + "执行了任务" + i + "~");
           }
         }
       });
     }
   }
   ```

注解池



### Android

#### 哪一个Layout性能最好？

- 布局层级：布局层级的深度越深，渲染性能就越低；
  1. LinearLayout顺序排列，简单，层级少；
  2. RelativeLayout元素位置是相互的，层级相对复杂；
  3. 结论：从布局层级比较，LL比RL性能好。

- 视图重绘：视图的重绘次数越多，性能越差；
  1. 视图改变时，触发Android视图重绘，
  2. RL重绘时，计算所有视图位置。
  3. LL重绘时，子视图线性排列，重绘少；
  4. 结论：从视图重绘比较，LL比RL性能好。

- 资源消耗：布局所需内存和CPU资源越多，性能越差。
  	1. 子视图重绘，导致更多资源和CPU消耗
  	1. 结论：从资源消耗比较，LL比RL性能好。

- 最终结论：

  1. 当布局很简单时，就使用简单的LinearLayout布局。
  2. 当布局存在嵌套，但不是很复杂时，使用RelativeLayout布局。
  3. 当布局非常复杂，使用ConstraintLayout布局。

#### Android四大组件有哪些？

- Activity

  - Activity是一个框架或者页面

    - Acitivity中使用intent进行通信
    - 每个Activity都必须要在AndroidManifest.xml配置文件中声明，否则系统不识别该Activity。

  - Activity的生命周期有哪些？

    启动Activity -> onCreate() -> onStart() -> onResume() -> onPause() -> onStop -> onDestroy() -> 关闭Activity

- Service



- Content Provider



- Broadcast Receiver

#### ContentProvider作为四大组件之一有什么作用？



#### Bundle的作用是什么？

- Bundle是Android中的一个类，用于<u>存储键值对形式的数据</u>。
- 常常用于在各个Activity或Fragment中，传递参数。

#### Fragment的生命周期



#### MVC  Model — View — Controller



#### MVP  Model — View — Presenter



#### MVVM Model — View — ViewModel 