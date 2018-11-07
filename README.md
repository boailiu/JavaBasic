# JavaBasic
**Java基础知识总结**<br>
作为Java开发人员，基础的永远是最重要的根基，所以准备记录下自己遇到的基础知识点，以此记录。

---
**接口与抽象类**<br>
* **接口**<br>
1.Java8之前接口中的方法都是抽象方法，没有具体的实现，默认修饰符是public；Java8之后接口中可以有默认的实现方法，用default,static进行修饰<br>
2.接口可以实现多继承接口，但是不能实现接口<br>
3.接口不能有构造器<br>
4.接口中的成员变量只能是public static final类型的<br>
5.接口中不能含有static静态代码块，Java8之后可以有静态方法<br>
* **抽象类**<br>
1.抽象类可以有默认的实现方法<br>
2.如果子类不是抽象类，那么需要实现抽象类所有声明的方法，否则子类也要用abstract进行修饰为抽象类<br>
3.抽象类可以有构造器<br>
4.抽象方法可以有public、protected、default修饰符<br>
5.抽象方法可以有main方法并且可以运行它<br>
6.抽象方法可以继承一个类，实现多个接口<br>
7.除了不能实例化抽象类之外，它和正常的类没有区别<br>
8.抽象类中可以有静态方法和静态代码块<br>
---

**内部类**<br>
* **静态内部类**<br>
1.不可访问外部的非静态资源，因为静态内部类对象的创建不依赖外部类，而外部类的非静态资源的创建是依赖外部类的，如果允许访问外部类非静态资源，则会产生矛盾<br>
2.可以有public static abstract class Demo
* **成员内部类**<br>
1.可以访问外部的所有资源（包括private和静态资源），但是本身内部不可以有静态属性（因为本身需要依靠外部类的实例化）<br>
2.当成员内部类与外部类有同名的变量或者方法时，会发生隐藏现象，默认访问的内部类中的变量，通过 外部类.this.变量名（方法名）进行访问<br>
* **局部内部类**<br>
局部内部类是指定义在一个方法中或者一个作用域内，它的访问权限只能是方法中或者作用域中<br>
1.不可被 访问修饰符(public protected private)和static修饰，只能访问final变量和形参
* **匿名内部类**<br>
1.匿名内部类是唯一没有构造器的类，没有静态资源，无法被访问修饰符和static修饰<br>
2.只能创建匿名内部类的一个实例<br>
3.创建的时候一定是在new的后面，大部分用户接口回调<br>
4.匿名内部类也只能访问final修饰的局部变量<br>
---

**线程池**<br>
 线程池主要处理流程:<br>
 1. 线程池判断**核心线程池**里的线程是否都在执行任务。如果不是，则创建一个新的工作线程来执行任务。如果核心线程池里的线程都在执行任务，则进入到下个流程<br>
 2.线程池判断**工作队列**是否已满。如果工作队列没有满，则将新提交的任务存储在工作队列中。如果工作队列已满，则进入下个流程。<br>
 3.线程池判断**线程池**中的线程是否都处于工作状态。如果没有，则创建一个新的工作线程来执行任务。如果已满,即达到线程池允许的最大线程数，则交给**饱和策略**来处理这个任务。<br>
 
 **ThreadPoolExecutor**<br>
 * **FixedThreadPool**<br>
 1.FixedThreadPoolExecutor被称为可重用固定线程数的线程池,它的corePoolSize和maximumPoolSize值相等<br>
 2.FixedThreadPoolExecutor使用**无界队列LinkedBlockingQueue**作为线程池的工作队列<br>
 3.由于使用无界队列，所以没有饱和策略，不会拒绝任务。<br>
 
 * **SingleThreadPoolExecutor**<br>
 1.SingleThreadPoolExecutor是单个线程的线程池，它的corePoolSize和maximumPoolSize值都为1<br>
 2.SingleThreadPoolExecutor使用**无界队列LinkedBlockingQueue**作为线程池的工作队列<br>
 
 * **CachedThreadPool**<br>
 1.CachedThreadPool是一个没有容量限制的线程池，它会根据需要创建新的线程执行任务，没有特定的corePool<br>
 2.CachedThreadPool的corePoolSize为0，maximumPoolSize值为Integet.MAX_VALUE<br>
 3.keepAliveTime设置为60秒，空闲的线程最多等待60秒，否则被回收<br>
 4.工作队列使用没有容量的**synchronousQueue**，这是一个没有容量的阻塞队列，每个插入操作必须等待另一个线程的对应移除操作。当任务提交的速度大于线程处理的速度，系统会不断的创建新的线程。在极端情况下，可能会因创建过多线程而耗尽cpu资源<br>
 
 * **ScheduledThreadPoolExecutor**<br>
 1.newScheduledThreadPool创建一个大小无限的线程池，支持定时以及周期性执行任务<br>
 2.使用**DelayedWorkQueue**作为工作队列，这是一个可延时执行阻塞任务的队列<br>
 ---
 
**并发包中的阻塞对列**<br>
Java并发包中的阻塞对列有7个，它们都是线程安全的<br>
* ArrayBlockingQueue:由数组结构组成的有界阻塞队列<br>
* LinkedBlockingQueue:由链表结构组成的有界阻塞队列<br>
* PriorityBlockingQueue:支持优先级排序的无界阻塞队列<br>
* DelayQueue:使用优先级队列实现的无界阻塞队列<br>
* SynchronousQueue:不存储元素的阻塞队列<br>
* LinkedTransferQueue:一个由链表组成的无界阻塞队列<br>
* LinkedBlockingDeque:一个由链表结构组成的双向阻塞队列<br>
---

**Java中的锁**<br>
* **重入锁 ReentrantLock** <br>

重入锁表示在同一个线程中，锁可以重复获得，同时，在释放锁的时候就需要多次释放锁。<br>
ReentrantLock的重要方法：<br>
lock()：获得锁，如果锁已经被占用，则等待。<br>
lockInterruptibly():获得锁，但**优先响应中断**。<br>
tryLock():尝试获得锁，如果成功，返回true，是在返回false。**该方法不等待，直接返回**。<br>
tryLock(long time, TimeUnit unit):在给定时间内尝试获得锁。<br>
unLock():释放锁。<br>
重入锁的搭档Condition条件，Condition包含的方法aWait()和singal()类似于Object对象的wait()和notify()方法。<br>


* **信号量 Semaphore** <br>

信号量为多线程协作提供了更为强大的控制方法，信号量可以指定多个线程，同时访问某一个资源。构造信号量对象时，必须要指定信号量的准入数，也就是同时能申请多少个许可。每个线程每次只允许申请一个许可时，就相当于指定了多少个线程可以访问某一个资源。<br>
Semaphore的重要方法：<br>
acquire():尝试获得一个准入的许可。若无法获得，则线程会等待，直到有一个线程释放一个许可或者当前线程被中断。<br>
acquireUninterruptibly():与acquire()类似，但是不响应中断。<br>
tryAcquire():尝试获得一个许可，如果成功返回true，失败直接返回false，它不会进行等待，立即返回结果。<br>
tryAcquire(long timeout, TimeUnit unit):给定一个等待的时间尝试获得许可，与tryAcquire()一样直接返回结果。<br>
release():释放一个许可。<br>


* **读写锁 ReadWriteLock** <br>

读写锁允许多个线程同时读，但是写写之间会阻塞。<br>
jdk中ReentrantReadWriteLock又有读锁readLock和写锁writeLock，可以分开操作。<br>


* **倒计数器 CountDownLatch** <br>

CountDownLatch是一个使用的多线程控制工具类，通常用来控制线程等待，它可以让一个线程等待**直到**倒计时结束，再开始执行。<br>
public CountDownLatch(int count) 接受一个整数作为参数，即当前这个计数器的计数个数。<br>
countDown() 执行一次countDown()方法，代表倒计时器-1 <br>


* **循环栅栏 CyclicBarrier** <br>
循环栅栏是另一个多线程并发控制实用工具。与CountDownLatch类似，它可以实现线程间的计数等待。<br>
public CyclicBarrier(int parties, Runnable barrierAction) <br>
CyclicBarrier可以接收一个参数作为barrierAction，就是当计数器一次计数完成后，系统会执行的动作。<br>

---

**Java中的并发容器**<br>

* **ConcurrentHashMap**<br>
线程安全的HashMap<br>
* **CopyOnWriteArrayList**<br>
这是一个List，适合读多写少的场景，效率高于vector<br>
由于读操作不会修改原有的数据，所以给读操作加锁是一种资源浪费。CopyOnWriteArrayList只有在写与写操作之间进行同步等待。<br>
CopyOnWrite在读操作时是读取的**原数据**，而在进行写操作时会进行一次**自我复制**，形成一个副本，而写操作不会对原数据进行修改，而是对副本数据进行修改，再用修改后的副本替换原来的数据，这样保证了写操作不影响读。<br>
因为内部实现的数组是**volatile**类型，所以修改之后读取线程可以立即察觉到这个修改（volatile的可见性）<br>
* **ConcurrentLinkedQueue**<br>
高效的并发队列，使用链表实现。可以看做是一个线程安全的linkedList。<br>
* **BlockingQueue**<br>
这是一个接口，jdk内部通过链表、数组等方式实现了这个接口。表示阻塞队列，非常适合用于数据共享的通道。<br>
ArrayBlockingQueue基于数组实现，因为数组有界，所以更适合做有界队列<br>
队列中放入元素，使用offer()和put()方法。offer()方法会立刻返回结果，put()方法则会进行阻塞。<br>
队列取出元素，使用poll()和take()方法。同样的，poll()会立刻返回结果，而take()方法则会进行阻塞。<br>
内部实现，使用了ReentrantLock和两个Condition（notEmpty,notFull）基于await()和signal()实现<br>
* **ConcurrentSkipListMap**<br>
跳表的实现。这是一个Map，使用跳表的数据结构进行快速查找。跳表内的数据是有序的，是一种以空间换时间的算法<br>
跳表首先是有序的，然后内部由多条链表组成，最底层的链表包含了所有元素，每上面一层都是下面一层的子集，所以根据最上层的元素大小，可以很方便的进行查找当前元素是在这个元素的左边还是右边，增加了查找速度。<br>
内部关键数据结构：Node节点-存储key和value，对应Map中的key和value，Node节点还有一个next指针节点。索引Index-它内部包装了Node，并增加了向下和向右的引用。HeadIndex-对于每一层的表头，还需要记录当前处于哪一层，所以用HeadIndex维护，表示头部的第一个Index，它继承自Index <br>





