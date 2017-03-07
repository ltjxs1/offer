### 1.什么情况会造成内存泄露

1) 当某个对象被定义为static的变量所引用，那么gc通常是不会回收这个对象所占有的堆内存的，如：
```
public class A{
   private static B b = new B();
}
```

2) static map，用一个对象作为key，然后修改了这个对象，导致hash变了，结果用之前那个对象作为key去取，取不到


### 2.在java中wait和sleep方法的不同？

- 等待时wait会释放锁，而sleep一直持有锁。
- wait通常被用于线程间交互，sleep通常被用于暂停执行。
- wait属于Object方法，sleep属于Thread方法。
