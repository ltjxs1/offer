### 更好的使用Java线程池

在多线程编程中创建线程池的时候，一般禁止使用`Executors.newFixedThreadPool(8)`方式创建线程池，这是一种偷懒的行为。一般使用

```

new ThreadPoolExecutor(int corePoolSize, int maximumPoolSize, long keepAliveTime, TimeUnit unit, BlockingQueue<Runnable> workQueue, ThreadFactory threadFactory, RejectedExecutionHandler handler)

```

这种方式创建。

构造函数里传入的参数将会直接影响线程池的效率，因此必须要知道这些参数的意义。

- corePoolSize: 线程池维持的线程数量,即使这些线程是空闲的,除非设置 `allowCoreThreadTimeOut` 为 `true`
- maximumPoolSize: 线程池允许的最大线程数量
- keepAliveTime: 当前线程数大于`corePoolSize`，多余的空闲线程存活时间
- unit: `keepAliveTime`参数的时间单位
- workQueue: 任务队列
- threadFactory: 线程创建工厂
- handler: 任务队列满了导致阻塞时新任务的拒绝策略

上面的解释是JDK的注释，写的也是云里雾里，下面进行一一解释。

**corePoolSize**

线程池默认初始化时，`allowCoreThreadTimeOut`为`false`, 也就是说默认情况下，线程池的线程数最小是`corePoolSize`, 即使这些线程是空闲的，数量也会维持在`corePoolSize`。线程池对象有个方法`allowCoreThreadTimeOut(boolean value)`, 当传入`true`的时候，表示核心线程池的线程在没有任务到达的时候，`keepAliveTime`时间后关闭，线程池里的线程数量就会小于`corePoolSize`。

**maximumPoolSize**

`maximumPoolSize` 表示线程池的最大线程数量。当线程池的数量达到`corePoolSize`，并且任务队列已经满了，则会继续创建新线程直到数量达到`maximumPoolSize`。但是请注意，当`workQueue`传入的是无界队列的时候，`maximumPoolSize`参数是不起作用的，线程池的最大数量会一直是`corePoolSize`。

**workQueue**

`workQueue`参数需要传入一个阻塞队列，队列分为有界队列（比如`ArrayBlockingQueue`）和无界队列（比如`LinkedBlockingQueue`），传入无界队列时，`maximumPoolSize`参数是不起作用的。

**handler**

配置拒绝策略，拒绝策略有：

- AbortPolicy    直接拒绝新任务，并抛出`RejectedExecutionException`异常
- CallerRunsPolicy    用当前线程的`execute`方法执行被拒绝的任务，如果执行器已经关闭则丢弃任务
- DiscardPolicy    默默地丢弃新到的任务
- DiscardOldestPolicy    丢弃最老的一个未执行的任务并执行当前任务

要知道，线程池初始化的时候，池子里是没有线程的。

那`corePoolSize`配置成多大合适呢？一般来说，CPU密集型任务可以少配置线程数，大概和机器的cpu核数相当。IO密集型时，大部分线程都阻塞，故需要多配置线程数，2*cpu核数
