# **Android开发面试问题**

React Native



#### Java

- ##### equals和==的区别

  对于==，基本数据类型，比较的是值是否相等，引用数据类型，比较的是对象地址是否相等。对于equal，默认对象地址。String，重写了方法，比较的是值是否相同。

- ##### 哪一个Layout性能最好？

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



##### Android四大组件有哪些？

- Activity

  - Activity的生命周期有哪些？

    启动Activity -> onCreate() -> onStart() -> onResume() -> onPause() -> onStop -> onDestroy() -> 关闭Activity

- Service



- Content Provider



- Broadcast Receiver



##### ContentProvider作为四大组件之一有什么作用？



##### Bundle的作用是什么？



##### HashMap



##### 解决多线程



##### MVC  Model — View — Controller



##### MVP  Model — View — Presenter



##### MVVM Model — View — ViewModel 



##### 如何解决同一个变量同时被多个线程改动的情况



##### Fragment的生命周期



##### 几种新建线程的方式