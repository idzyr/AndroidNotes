# 多线程和异步任务

## 线程池

### 基本线程池

创建线程池，主要是利用ThreadPoolExecutor这个类。设置好几个参数就可以创建一个基本的线程池，而之后的各种线程池都是在这种基本线程池的基础上延伸的。

**构造方法；**

- `ThreadPoolExecutor(int corePoolSize,int maximumPoolSize,long keepAliveTime,TimeUnit unit,BlockingQueue<Runnable> workQueue,ThreadFactory threadFactory)`创建基本线程池
  - 参数
    - `int corePoolSize` 核心线程数
    - `int maximumPoolSize `最大线程池大小
    - `long keepAliveTime `保持活动时间，是非核心线程空闲时要等待下一个任务到来的时间
    - `TimeUnit unit` 上面保持活动时间时间单位
    - `BlockingQueue<Runnable> workQueue `任务队列
    - `ThreadFactory threadFactory `线程工厂，可用于设置线程名字等等，一般无须设置该参数。

### 可重用固定线程数

Executors类中的创建方法：

- `Executors.newFixedThreadPool(int corePoolSize)` 创建可重用固定线程数
  - 参数
    - `int corePoolSize` 核心线程数
  - 返回值
    - ExecutorService

### 线程池部分方法

- `shutDown()` 关闭线程池，不影响已经提交的任务
- `shutDownNow()` 关闭线程池，并尝试去终止正在执行的线程
- `allowCoreThreadTimeOut(boolean value) 允许`核心线程闲置超时时被回收
- `submit()` 一般情况下我们使用execute来提交任务，但是有时候可能也会用到submit，使用submit的好处是submit有返回值。
- `execute(runnable)` 执行任务
- `beforeExecute()` - 任务执行前执行的方法
- `afterExecute()` -任务执行结束后执行的方法
- `terminated()` -线程池关闭后执行的方法