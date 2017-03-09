### 1.Spring @Autowire和@Resource的区别

在@Autowire使用时，默认使用by-Type的方式进行注入(类名注入)

而@Resource，默认使用by-Type的方式注入，但使用by-Name方式时，相比@Autowire较方便(类名和注解名注入)

@Autowire用于属性、构造器、多参数方法注入，可以通过@Qualifer变为by-Name方式

@Resource则支持属性、setter方法上的使用：如果名字没有明确指定，默认名从那个字段名或者方法名中推断出。如果是字段，就获取这个字段名；如果是setter方法，其获取bean的属性名。

所以，你在注入构造器与多参数方法时，请使用@Autowire与@Qualifer进行配合

### 2.spring aop底层实现方式

动态代理

### 3.spring事务的实现原理

动态代理

所谓事务传播行为就是多个事务方法相互调用时，事务如何在这些方法间传播。Spring 支持 7 种事务传播行为：

PROPAGATION_REQUIRED 如果当前没有事务，就新建一个事务，如果已经存在一个事务中，加入到这个事务中。这是最常见的选择。

PROPAGATION_SUPPORTS 支持当前事务，如果当前没有事务，就以非事务方式执行。

PROPAGATION_MANDATORY 使用当前的事务，如果当前没有事务，就抛出异常。

PROPAGATION_REQUIRES_NEW 新建事务，如果当前存在事务，把当前事务挂起。

PROPAGATION_NOT_SUPPORTED 以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。

PROPAGATION_NEVER 以非事务方式执行，如果当前存在事务，则抛出异常。

PROPAGATION_NESTED 如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与

PROPAGATION_REQUIRED 类似的操作。
