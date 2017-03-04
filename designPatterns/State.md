### 状态设计模式

>现在姜小码有这样一个需求，让王小码写一个方法判断一个学生该上什么学校。

王小码2分钟后就给出了代码：

```
public class Person {
    private int age;

    public Person(int age) {
        this.age = age;
    }

    public void printSchool() {
        if (this.getAge() < 6) {
            System.out.println("小于6岁不能上学!");
        } else if (this.getAge() >=6 && this.getAge() < 11) {
            System.out.println("该上小学了!");
        } else if (this.getAge() >= 11 && this.getAge() < 15) {
            System.out.println("该上初中了!");
        } else if(this.getAge() >= 15 && this.getAge() < 19) {
            System.out.println("该上高中了!");
        } else if (this.getAge() >= 19) {
            System.out.println("该上大学了!");
        }
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

姜小码很高兴，并把王小码打了一顿。

假如姜小码又有新需求，判断这个学生在上几年级。总不能写18个判断分支吧。这种写法很显然破坏了**单一职责原则**，虽然下面要说到的**状态设计模式**增加了复杂性，但是易于扩展，符合面向对象的设计原则。

状态设计模式就是为了解决这类判断分支过多的问题，达到责任分解的目的。

状态设计模式将特定的状态相关行为放入一个对象中，由于所有与状态相关的代码都在某个State中，所以通过定义新的子类可以很容易增加状态和转换。

改造后的代码：

包结构

```
-state //状态设计模式
  -states
    -AgeState.java //状态抽象类
    -PrimaryState.java //小学
    -MiddleState.java //初中
    -HighState.java //高中
    -UniversityState.java //大学
  -Person.java
  -PersonTest.java
```

抽象状态

```
public abstract class AgeState {

    public abstract void judge(Person person);
}
```

小学状态

```
public class PrimaryState extends AgeState {
    @Override
    public void judge(Person person) {
        if (person.getAge() < 6) {
            System.out.println("年纪太小不足6岁,不能上学!");
        } else if (person.getAge() >= 6 && person.getAge() < 11) {
            System.out.println("该上小学了!");
        } else {
            person.setAgeState(new MiddleState());
            person.printSchool();
        }
    }
}
```

初中状态

```
public class MiddleState extends AgeState {
    @Override
    public void judge(Person person) {
        if (person.getAge() >= 11 && person.getAge() < 15) {
            System.out.println("该上初中了!");
        } else {
            person.setAgeState(new HighState());
            person.printSchool();
        }
    }
}
```

高中状态

```
public class HighState extends AgeState {
    @Override
    public void judge(Person person) {
        if (person.getAge() >= 15 && person.getAge() < 19) {
            System.out.println("该上高中了!");
        } else {
            person.setAgeState(new UniversityState());
            person.printSchool();
        }
    }
}
```

大学状态

```
public class UniversityState extends AgeState {
    @Override
    public void judge(Person person) {
        if (person.getAge() >= 19) {
            System.out.println("该上大学了!");
        }
    }
}
```

Person类

```
public class Person {

    private int age;
    private AgeState ageState;

    public void printSchool() {
        this.ageState.judge(this);
    }

    public Person(int age) {
        this.age = age;
        this.ageState = new PrimaryState();
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public AgeState getAgeState() {
        return ageState;
    }

    public void setAgeState(AgeState ageState) {
        this.ageState = ageState;
    }
}

```

测试：

```
public class PersonTest {

    public static void main(String[] args) {
        Person p1 = new Person(12);
        p1.printSchool();

        Person p2 = new Person(18);
        p2.printSchool();

        Person p3 = new Person(3);
        p3.printSchool();

        Person p4 = new Person(23);
        p4.printSchool();
    }
}
```

测试输出：

```
该上初中了!
该上高中了!
年纪太小不足6岁,不能上学!
该上大学了!
```

这样改完，以后扩展个研究生，博士，博士后还是很容易的。
