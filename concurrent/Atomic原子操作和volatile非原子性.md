首先，我们要理解什么叫原子操作，原子操作可以理解为：在多线程操作同一对象时，在非程序代码加锁状况下，保证被操作对象是结果是符合预期的。

翻译为人话就是：一个数，很多线程去同时修改它，不加sync同步锁，就可以保证修改结果是正确的。

那它是如何保证的呢？我们先了解一个叫CAS的东西：

CAS（Compare and swap）：比较和替换是设计并发算法时用到的一种技术。简单来说，比较和替换是使用一个期望值和一个变量的当前值进行比较，如果当前变量的值与我们期望的值相等，就使用一个新值替换当前变量的值。CAS是一种系统原语（所谓原语属于操作系统用语范畴。原语由若干条指令组成的，用于完成一定功能的一个过程。primitive or atomic action 是由若干个机器指令构成的完成某种特定功能的一段程序，具有不可分割性·即原语的执行必须是连续的，在执行过程中不允许被中断）。CAS是Compare And Set的缩写。CAS有3个操作数，内存值V，旧的预期值A，要修改的新值B。当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做。
可以说，原子操作正是靠CAS算法保证的。可能有人会有疑问：CAS是比较替换算法，会不会同时有两个线程同时比较且同时替换？答案当然是：不会。

为什么不会？我们来看一下下面的内容，前方高能，需要操作系统的知识：

1、原语由若干条指令组成的，用于完成一定功能的一个过程。

2、即原语的执行必须是连续的，在执行过程中不允许被中断。

在x86 平台上，CPU提供了在指令执行期间对总线加锁的手段。CPU芯片上有一条引线#HLOCK pin，如果汇编语言的程序中在一条指令前面加上前缀'LOCK'，经过汇编以后的机器代码就使CPU在执行这条指令的时候把#HLOCK pin的电位拉低，持续到这条指令结束时放开，从而把总线锁住，这样同一总线上别的CPU就暂时不能通过总线访问内存了，保证了这条指令在多处理器环境中的原子性。
所以，不会存在两个线程同时比较、同时替换。另外，因为CAS是基于乐观锁的，也就是说当写入的时候，如果寄存器旧值已经不等于现值，说明有其他CPU在修改，那就继续尝试。所以这就保证了操作的原子性。因此在大请求量的性能表现上，CAS乐观锁也是可以大大提高吞吐量的。


Atomic正是采用了CAS算法，所以可以在多线程环境下安全地操作对象。

总之，原子操作的基石是：CPU对总线加锁，加锁的方式叫：拉低电位（一串0101010100101呼啸而过）。


然而，volatile是Java的关键字，官方解释：volatile可以保证可见性、顺序性、一致性。

下面解读一下：

可见性：volatile修饰的对象在加载时会告知JVM，对象在CPU的缓存上对多个线程是同时可见的。

顺序性：这里有JVM的内存屏障的概念，简单理解为：可以保证线程操作对象时是顺序执行的，详细了解可以自行查阅。

一致性：可以保证多个线程读取数据时，读取到的数据是最新的。（注意读取的是最新的数据，但不保证写回时不会覆盖其他线程修改的结果）


基于上面的信息，大概可以初步了解volatile多线程下非原子性了。
