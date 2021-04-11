---
title: "Day11"
date: 2021-04-10T22:36:59+08:00
lastmod: 2021-04-10
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### **new 类名().new 类名()** 与 **new 类名.new** 这两种方式有什么区别?

**new 类名().new 类名()**

创建成员内部类

**new 外围类类名.new 静态内部类类名()**

创建静态内部类

### 局部内部类有什么优缺点?

**优点**

绝对的封装性，并且可以少创建一个 **class**, 相对来说简单一点

**缺点**

局部内部类作用域仅限于方法，如果别的类， 别的方法也想用这个类 做不到

### ![20210410192027](https://img.fengqigang.cn//img/20210410192027.png) 可以进行吗?为什么?

可以，**任何时候都有父类**，哪怕是实现了一个接口

### ![20210410192444](https://img.fengqigang.cn//img/20210410192444.png) , 为什么 **a++** 无法执行?

1. 生命周期的问题

方法的局部变量的生命周期和方法同生共死, 方法出栈就销毁

但是 **局部内部类的方法会创建对象**

于是出现方法出栈后，局部变量销毁了，但是对象仍然需要使用该局部变量的情况 

为了解决这种生命周期的冲突，**jvm** 会在创建局部内部类对象时，把方法的局部变量作为对象的成员变量加了进去

![20210410200236](https://img.fengqigang.cn//img/20210410200236.png)

2. 这个成员变量和局部变量值同步的问题

如果在局部内部类当中， 把这个局部变量给修改了，那就必须同步这个修改，否则程序就有问题

但是这样显然太复杂了，**java** 的开发都觉得不想做了，于是直接把这个局部变量声明为 **final** 做为一个常量，直接不修改，就不需要考虑同步问题

**Java8** 之前，如果想用局部内部类访问方法的局部变量， 该局部变量必须声明为 **final**

**Java8** 之后， 这个限制被解除了，改为在底层直接加上 **final**, 不需要程序再加了

这就是 **语法糖**

### **匿名内部类** 和 **lambda** 的局部变量有什么特殊的地方?

**匿名内部类** 和 **lambda** 本质的是 **局部内部类**

它们的局部变量仍然是 **final** 修饰的

### 内部类实现多继承的思路是什么?

![20210410200710](https://img.fengqigang.cn//img/20210410200710.png)

### 内部类有什么优缺点?

**优点**

1. 无条件地访问外围类的所有元素

**成员内部类**, **静态内部类**, **局部内部类**, **匿名内部类** 都可以无条件访问

2. 隐藏类

可以用 **private**, **protected** 修饰类

**private** 修饰成员内部类, 提供 **public** 的创建对象方法

3. 实现多继承

可以创建多个成员内部类继承外部多个类

然后创建内部类对象，实际上就是外围类继承了多个类的成员

![20210410200710](https://img.fengqigang.cn//img/20210410200710.png)

4. 通过匿名内部类来优化简单的接口实现

**缺点**

1. 语法复杂


**内部类就应该给外围类用，不需要给外部类用，给它用是有风险的**

### ![20210410201549](https://img.fengqigang.cn//img/20210410201549.png) 如何调用输出"我在学习局部内部类"?


![20210410201738](https://img.fengqigang.cn//img/20210410201738.png)


### 什么是匿名类(Anonymous Class)?

如果一个类没有名字，那么这个类就是匿名类

### 如何定义一个匿名内部类?


```java
new 接口名/类名(普通类, 抽象类) () {
};
```

![20210410202339](https://img.fengqigang.cn//img/20210410202339.png)

### ![20210411205439](https://img.fengqigang.cn//img/20210411205439.png) 如何实现? (朴素做法)

1. **Outer** 是一个 **class**, 类名点调用方法，代表这个方法是静态成员方法

2. 链式调用后面又调用了一个 **show** 方法，这意味着 **Outter.method()** 方法的返回值是对象

3. **show** 方法是接口 **Inter** 的抽象方法，所以 **method** 方法的返回值就是接口的实现类对象

```java
public class Demo {
    public static void main(String[] args) {
        Outer.method().show();
    }
}

interface Inter {
    void show();
}

class Outer {
    public static InterImpl method() {
        return new InterImpl();
    }
}

class InterImpl implements Inter {
    @Override
    public void show() {
        System.out.println("hello world!");
    }
}
```

![20210411210541](https://img.fengqigang.cn//img/20210411210541.png)

### ![20210411205439](https://img.fengqigang.cn//img/20210411205439.png) 如何实现? (高端做法)

1. **Outer** 是一个 **class**, 类名点调用方法，代表这个方法是静态成员方法

2. 链式调用后面又调用了一个 **show** 方法，这意味着 **Outter.method()** 方法的返回值是对象

3. 直接返回这个接口对象，重写 **show()** 方法

```java
public class Demo {
    public static void main(String[] args) {
        Outer.method().show();
    }
}

interface Inter {
    void show();
}

class Outer {
    public static Inter method() {
        return new Inter() {
            @Override
            public void show() {
                System.out.println("hello, world!");
            }
        };
    }
}
```

![20210411211308](https://img.fengqigang.cn//img/20210411211308.png)

### ![20210411211838](https://img.fengqigang.cn//img/20210411211838.png) 如何实现将匿名内部类作为 **test()** 方法的参数，重写 **eat()** 方法?

```java
public class Demo {
    public static void main(String[] args) {
        test(new AbstractPerson() {
            @Override
            void eat() {
                System.out.println("我是人，我要吃饭");
            }
        });
    }

    public static void test(AbstractPerson as) {
        as.eat();
    }
}

abstract class AbstractPerson {
    int age;
    String name;

    void eat() {
    }
    ;
}
```

![20210411212056](https://img.fengqigang.cn//img/20210411212056.png)

### ![20210411213537](https://img.fengqigang.cn//img/20210411213537.png)如何通过创建出父类成员变量赋值过的匿名内部类对象?

```java
public class Demo {
    public static void main(String[] args) {
        new AbstractPerson(18, "zhangsan") {
            @Override
            void eat() {
                System.out.println(this.age + "\t" + this.name);
            }
        }.eat();
    }

    public static void test(AbstractPerson as) {
        as.eat();
    }
}

abstract class AbstractPerson {
    int age;
    String name;
    public AbstractPerson() {
    }
    public AbstractPerson(int age, String name) {
        this.age = age;
        this.name = name;
    }
    void eat() {
    }
}
```

![20210411213811](https://img.fengqigang.cn//img/20210411213811.png)

```java
public class Demo {
    public static void main(String[] args) {
        test(new AbstractPerson(18, "zhangsan") {
            @Override
            void eat() {
                System.out.println(this.age + "\t" + this.name);
            }
        });
    }

    public static void test(AbstractPerson as) {
        as.eat();
    }
}

abstract class AbstractPerson {
    int age;
    String name;

    public AbstractPerson(){}

    public AbstractPerson(int age, String name){
        this.age = age;
        this.name = name;
    }

    void eat() {
    };

}
```

![20210411213934](https://img.fengqigang.cn//img/20210411213934.png)

### ![20210411214227](https://img.fengqigang.cn//img/20210411214227.png) 匿名内部类 **new 类名()** 这个括号有什么用?

这个括号可以传参数，给父类成员赋值

### 什么是 **lambda** 表达式?

**lambda** 是 **JDK8** 的一个新特性

**lambda** 就是匿名内部类更进一步，语法上更简洁了，代码更优雅了

### **lambda** 有什么需要注意的地方?

1. 它是用来取代 **接口的匿名内部类**, **不能取代普通类和抽象类的匿名内部类**

2. 对接口有严格的要求:

**有且仅有一个抽象方法需要子类实现**, 这种接口被称这为 **功能接口** (function interface)

### 如何判断一个接口是否是功能接口?

用注解去检测

@FunctionInterface

有且仅有一个抽象方法需要子类实现, 称之为 **功能接口**

![20210411215027](https://img.fengqigang.cn//img/20210411215027.png)

### **lambda** 表达式与 **功能接口** 有什么关系?

**lambda** 表达式是在方法内部创建功能接口的 **实现类对象**

### **lamba** 语法是什么?

```java
() -> {}
```

**()** 是形参列表，无需传入实际参数, 功能接口中那个唯一的抽象方法的形参列表

**->** 是 **lambda** 运算符, 可以读作 **goes to **

**{}** 中放的是抽象方法重写的方法体

### 为什么要求功能接口中有且仅有一个抽象方法?

因为 **lambda** 方法中型参表只有一个

方法体也只有一个， 没办法重写两个方法，只能重写一个

### ![20210411215815](https://img.fengqigang.cn//img/20210411215815.png) 如何采取直接告诉该对象的类型，直接用接口引用指向它?

```java
public class Demo {
    public static void main(String[] args) {
        IA ia = () -> {
            System.out.println("hello world!");
        };
        ia.test();
    }
}

@FunctionalInterface
interface IA {
    void test();
}
```

![20210411220028](https://img.fengqigang.cn//img/20210411220028.png)

### ![20210411215815](https://img.fengqigang.cn//img/20210411215815.png) 如何采取直接告诉该对象的类型，不接收它，并调用 **test** 方法?

```java
public class Demo {
    public static void main(String[] args) {
        ((IA) () -> {
            System.out.println("hello world!");
        }).test();
    }
}

@FunctionalInterface
interface IA {
    void test();
}
```

![20210411220259](https://img.fengqigang.cn//img/20210411220259.png)

### ![20210411220734](https://img.fengqigang.cn//img/20210411220734.png) 这里的数据类型可以省略吗? 为什么?

可以，**lambda** 表达式已经明确知道用哪个接口，哪个抽象方法，所以形参列表中的数据类型是多余的， 可以省略的

![20210411221034](https://img.fengqigang.cn//img/20210411221034.png)

### ![20210411221146](https://img.fengqigang.cn//img/20210411221146.png) 这里的括号可以省略吗? 为什么?

可以, 如果这个参数 **只有一个** ，那么这个小括号是 **多余的**

如果 **没有参数** 和 **多个参数** , 不可省略小括号

![20210411221358](https://img.fengqigang.cn//img/20210411221358.png)

![20210411221506](https://img.fengqigang.cn//img/20210411221506.png)

### ![20210411221550](https://img.fengqigang.cn//img/20210411221550.png) 可以这样写吗?

**可以**, 在 **lambda** 表达式重写方法体中 **只有一条语句** ，**可以省略大括号**

### ![20210411221954](https://img.fengqigang.cn//img/20210411221954.png) 可以这样写吗? 为什么?

如果这个抽象方法是有返回值的，并且它的返回值语句只有一行，那么 **return** 就不需要了

### ![20210411222454](https://img.fengqigang.cn//img/20210411222454.png) 可以这样写吗? 为什么?

可以，把方法的实现，指向一个已经存在的方法中是可以的

### 如何判断 **已存在的方法** 和 **功能接口中的抽象方法** 是一样的?

只用看 **返回值类型** 和 **形参列表**

### ![20210411222855](https://img.fengqigang.cn//img/20210411222855.png)可以这样写吗?为什么?

在调用其他方法时，可以用 **方法归属者::方法名**

### 如何判断一个方法的归属者?

1. 成员方法

属于对象， 所以需要先创建对象， 再指向

![20210411223440](https://img.fengqigang.cn//img/20210411223440.png)

2. 静态成员方法，属于类，直接类名放上去

![20210411223142](https://img.fengqigang.cn//img/20210411223142.png)


