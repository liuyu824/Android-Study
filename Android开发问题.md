# **Android开发问题**

### Java

#### Java的四大特性

封装、继承、多态、抽象



#### equals和==的区别

对于==，基本数据类型，比较的是值是否相等，引用数据类型，比较的是对象地址是否相等。对于equal，默认对象地址。String，重写了方法，比较的是值是否相同。





#### HashMap底层实现原理



 



#### 变量被多线程改动

- Synchronized关键字最主要有以下3种应用方式，

  - 修饰实例方法

    作用于当前实例加锁，进入同步代码前要获得当前实例的锁,

    实例对象锁就是用synchronized修饰实例对象中的实例方法，注意是实例方法不包括静态方法，如下。

    ```java
    public class AccountingSync implements Runnable{
        //共享资源(临界资源)
        static int i=0;
    
        /**
         * synchronized 修饰实例方法
         */
        public synchronized void increase(){
            i++;
        }
        @Override
        public void run() {
            for(int j=0;j<1000000;j++){
                increase();
            }
        }
        public static void main(String[] args) throws InterruptedException {
            AccountingSync instance=new AccountingSync();
            Thread t1=new Thread(instance);
            Thread t2=new Thread(instance);
            t1.start();
            t2.start();
            t1.join();
            t2.join();
            System.out.println(i);
        }
        /**
         * 输出结果:
         * 2000000
         */
    }
    ```

  - 修饰静态方法

    作用于当前类对象加锁，进入同步代码前要获得当前类对象的锁

  - 修饰代码块

    指定加锁对象，对给定对象加锁，进入同步代码库前要获得给定对象的锁。



#### 悲观锁与乐观锁（顾名思义）

悲观锁：

在每次使用变量值时，都默认别的线程已经改变过了。在使用时就对变量进行上锁，别的进程使用时对遭遇阻塞。直到此线程使用完成，释放锁，别的线程再使用。

乐观锁

#### 锁升级机制



#### 几种新建线程的方式

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

6. 实现Callable接口
           通过自定义类（这里起名为：MyCallable），实现Callable接口，重写call方法（call方法可以理解为线程需要执行的任务），并且带有返回值，这个返回表示一个计算结果，如果无法计算结果，则引发Exception异常。

       

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

  - Service用于在后台执行长时间运行的操作，即使用户切换到其他应用或锁屏，这些操作也能继续进行。Service没有用户界面，它可以在后台执行耗时的任务或监听网络变化等。Service有两种状态：started（启动）和bound（绑定）。


- Content Provider
  - Content Provider用于在应用程序之间共享数据。它提供了一个统一的接口来访问数据，这些数据可能存储在数据库、文件或其他地方。Content Provider允许不同的应用程序访问和修改共享数据。


- Broadcast Receiver
  - Broadcast Receiver用于接收系统或应用程序发出的广播消息。它可以用来接收通知，如网络变化、电池电量低等。Broadcast Receiver不提供用户界面，但可以启动Activity或Service来响应接收到的广播。


#### ContentProvider作为四大组件之一有什么作用？

内容提供程序有助于应用管理其自身和其他应用所存储数据的访问，并提供与其他应用共享数据的方法。

#### Handler机制

描述

#### Bundle的作用是什么？

- Bundle是Android中的一个类，用于<u>存储键值对形式的数据</u>。
- 常常用于在各个Activity或Fragment中，传递参数。

#### Fragment的生命周期

1. Fragment的生命周期包含11个，其中有6个是和Activity的生命周期是相同的（onCreate()、onStart()、onResume()、onPause()、onStop（）、onDestroy（）），还有5个如下：
2. onAttach（）：当Fragment和Activity进行关联的时候调用；

2. onCreateView（）：加载Fragment相关的布局视图的时候调用；

3. onActivityCreated（）：对应的Activity已经创建的时候调用；

4. onDestroyView（）：清除Fragment相关的布局视图的时候调用；

5. onDetach（）：当Fragment和Activity解除关联的时候调用；

#### MVC  

Model — View — Controller



#### MVP  

Model — View — Presenter



#### MVVM 

Model — View — ViewModel



### 代码

#### 字符串拆解并按顺序排序

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");

        System.out.println("------------");

        /**
         * " abc12d3456ef789gh" ->"alb203d405f6g7h89"
         */

        String originStr = "abc12d3456ef789gh";
        int orgStrLength = originStr.length();
        // 新建两个ArrayList，用于存放数字与英语
        ArrayList<String> engArr = new ArrayList<>();
        ArrayList<String> numArr = new ArrayList<>();

        for (int i = 0; i < orgStrLength; i++) {
            if ("123456789".contains(String.valueOf(originStr.charAt(i)))){
                numArr.add(String.valueOf(originStr.charAt(i)));
            } else {
                engArr.add(String.valueOf(originStr.charAt(i)));
            }
        }

        int engArrLength = engArr.size();
        int numArrLength = numArr.size();

        String finalStr = "";
        for (int i = 0; i < (Math.max(engArrLength, numArrLength)); i++) {
            if (i < (Math.min(engArrLength, numArrLength))){
                finalStr += engArr.get(i);
                finalStr += numArr.get(i);
            } else {
                if (engArrLength > numArrLength){
                    finalStr += engArr.get(i);
                } else {
                    finalStr += numArr.get(i);
                }
            }
        }
        System.out.println(finalStr);
    }
}
```

#### 数组排序

```java
/**
* 要求：
* nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
* 输出：[1,2,2,3,5,6]
*/

int[] nums1 = new int[]{1,2,3,0,0,0};
int[] nums2 = new int[]{2,5,6};
int[] finalNums = new int[6];

// 获取每个数组的长度
int nums1Length = nums1.length;
int nums2Length = nums2.length;
for (int i = 0; i < nums1Length; i++) {
  if (nums1[i] != 0){
    finalNums[i] = nums1[i];
  }
}
for (int i = 3; i < nums2Length+3; i++) {
  finalNums[i] = nums2[i-3];
}
Arrays.sort(finalNums);
System.out.println(Arrays.toString(finalNums));
```

