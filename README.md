# 贱指offer

#待分类问题

1.项目使用的框架

2.有什么优化

3.项目遇到的坑

3.1 并发中遇到哪些问题

3.2 职业规划

3.3 说说你项目中印象比较深刻的bug

4.如何在项目中使用缓存

5.公司项目流程图

6.mq在项目中如何使用

7.hash一致性分片的好处

8.HashMap源码

9.put流程

10.扩容线程的5种状态如何切换

11.线程是否可以重复启动，会有什么后果。

12.synchronized 和 lock的区别

13.悲观锁、乐观锁，如何自己实现一个乐观锁

14.spring aop底层实现方式

15.spring事务的实现原理

16.事务的特性，4种隔离级别

17.http请求可能返回的状态码

18.post和get的区别

19.如何分辨一个对象是否为垃圾

20.是否可以手动回收

21.不可以手动回收，这个方法有什么用？

22.手写单例

23.学生表，班级学生关系表，查出所有班级学生大于90分的个数大于10的班级。

24.链表的逆转

25.一次循环查找出字符串中第一个不重复的字符

26.为何离职

27.自身优势

28.Mysql执行计划

29.慢sql

30.快排，堆排，归并排序，基数排序

31.线程的生命周期

32.单例在哪些场景中用到

33.线程启动的底层实现

34.wait()方法是哪个类的，为什么不把wait()方法放在Thread类，而是Object？

35.线程的实现方式

36.线程池底层是怎么实现的

37.线程池的两种创建方式

38.讲讲线程池coreSize和max的关系

39.线程池拒绝策略

40.二分查找

41.二叉排序树

42.在main方法中怎么调用单例实例

43.反射原理

44.spring ioc原理

45.TCP协议3次握手，4次挥手

45.1 TCP为什么是可靠的

46.SQL group by、having

47.数据库索引

48.java集合

49.List有哪些实现类，并描述数据结构，Map有哪些实现类，并描述数据结构

50.数据库索引

51.重写equals方法一定要重写hashcode方法吗

52.jvm启动时发生了那些事

53.HashMap和HashTable的区别。

54.TCP窗口是什么

55.TCP为什么比UDP慢

56.一个用户表 1亿条记录，如何快速找出某1万用户

57.算法：链表相交

58.如何避免HashMap resize

59.画一下线程的流程图

60.算法：一中间高两边低的数组找出峰值

61.一个数组，有两个数只出现一次，其他元素都出现两次以上，找出这两个数

62.HashMap实现原理，get的时间复杂度

63.spring 动态代理

64.CPU内存和缓存的工作方式

65.java 类加载机制

66.mysql递归树查询实现语句

67.cglib和jdk proxy区别

68.类锁，对象锁

69.异常结构物

70.事务的隔离级别，情景分析

71.LinkedHashMap使用场景

72.ThreadLocal 应用场景

73.同一进程的不同线程，哪些内容可以共享

74.字符串格式化，去掉首尾的空格，以及字符串中间连续的空格，但中间的只保留最后一个空格。比如： " i love meituan ",格式化后："ilove meituan”.

75.常用linux命令

76.单例模式的双重检查锁定写法

77.zookeeper原理

78.linux软连接和硬链接，如何查看cpu，内存，java。awk，top

79.数据库索引，复合索引

80.StringBuffer和StringBuilder的区别

81.螺旋矩阵算法

82.jvm调试，内存优化

83.Spring @Autowire和@Resource的区别

84.URL长度限制

85.volitile关键字作用

86.java 深克隆浅克隆

87.算法：查找链表倒数第K个节点

--------------------------------------------------------
88.spring 模块划分

89.应用上下文的集中实现方式

90.FutureTask的实现原理

91.awk实现文件合并

92.mysql 的锁

93.FactoryBean和BeanFactory的区别

94.HashMap和ConcurrentHashMap的线程安全问题

95.数据库事务的CAS

96.约瑟夫环的编程

97.中国有100G数据，美国有100G数据，如何对比数据是否一致？

98.如何判断链表是否有环

99.找出数组中第K大的数

100.java中的引用有几种?
4种。
强引用：强引用有引用变量指向时永远不会被垃圾回收，JVM宁愿抛出OutOfMemory错误也不会回收这种对象。
弱引用：弱引用也是用来描述非必需对象的，当JVM进行垃圾回收时，无论内存是否充足，都会回收被弱引用关联的对象
虚引用：如果一个对象与虚引用关联，则跟没有引用与之关联一样，在任何时候都可能被垃圾回收器回收
软引用：如果一个对象具有软引用，内存空间足够，垃圾回收器就不会回收它；如果内存空间不足了，就会回收这些对象的内存。只要垃圾回收器没有回收它，该对象就可以被程序使用。

101.Java中的threadlocal是怎么用的? threadlocal中的内部实现是怎么样的? 哪种引用?

102.java中的"final"关键字在多线程的语义中，有什么含义

103.说说nio的架构，为什么变快了，说说select和buffer都是怎么用的？
           1.在操作系统中的实现原理? 如果都是cpu轮训话，会不会对cpu影响太大?
           2.应用到了linux中的什么特性?

104.nio中， 如果不显式的调用 system.gc() 那会出现什么问题？

105.jvm的垃圾回收分为哪些种类？每一种都是怎么去实现的？讲述一下G1的回收策略？

106.jvm中的参数分为哪些种类，都是做什么的？jvm的监控怎么做？实际项目上线以后的监控怎么做？

107.JVM中，如果把堆内存参数配置的超过了本地内存，会怎么样？

108.JVM中的内存结构分为哪些方面？

109.栈空间是怎么样的？每个线程只有一个栈吗？

110.栈空间的内部结构是怎么样的？

111.堆内存为什么要设计为分代？

112.ArrayList的实现原理，如何测试ArrayList动态分配内存中带来的内存、cpu变化

113.ArrayList是不是线程安全的? 怎么实现线程安全的?

114.synchronized和lock有什么区别？

115.volatile的作用，如果volatile修饰的对象经过了大量的写，会出现什么问题？

116.String的+和StringBuilder有什么区别? 放在循环中有什么问题？

117.日志打印的过程中，使用String的+操作和使用占位符输出，对性能上有什么区别

117.SimpleDateFormat如果是一个全局变量的话，有什么问题？
        SimpleDateFormat是非线程安全的
118.HashMap的操作中，直接使用keySet()遍历有什么问题
        EntrySet


119.linux中awk命令的使用？

120.nginx是多线程还是单线程？

121.linux中如何监控和查看内存、cpu情况？

122.负载分为哪些类别和层次？你们项目中是怎么用的？

123.mq是如何使用的？

124.http协议建立连接的过程是怎么样的？

125.https建立连接的的过程是怎么样的？

126.forward和redirect有什么区别？

127.linux如何实现nginx的高性能？有什么特性被应用了？直接来说，就是基于linux的网络编程

128.数据流的锁级别，乐观锁和悲观锁的概念，是不是只有悲观锁？

129.数据库如何实现事务？

130.有没有什么研究深入的技术，或者比较满意的项目？
