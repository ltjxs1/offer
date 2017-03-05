### 1.什么情况会造成内存泄露

1) 当某个对象被定义为static的变量所引用，那么gc通常是不会回收这个对象所占有的堆内存的，如：
```
public class A{
   private static B b = new B();
}
```

2) static map，用一个对象作为key，然后修改了这个对象，导致hash变了，结果用之前那个对象作为key去取，取不到
