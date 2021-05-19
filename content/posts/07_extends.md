---
title: "07_extends"
date: 2021-04-06T23:03:23+08:00
lastmod: 2021-04-06
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 什么是默认导包, 隐式导包?

**java.lang** 包下的所有类，是 **java** 的核心类，它会自动隐式导入，不需要再写导包语句


### If I really need both `Date` classes in `java.util` and `java.sql`, what can I do?

use the full package name with every class name:

```java
public class PackageTest {
    public static void main(String[] args) {
       var deadline = new java.util.Date();
       var today = new java.sql.Date((long)123);
    }
}
```



### 什么是面向过程与面向对象?

面向过程 procedureal oriented programming

面向对象 oop

**面向过程的编程思想**

即程序是"动词"的集合，即程序功能是由一系列有序的动作来完成

**面向对象的编程思想**

即程序是由一系列的对象+对象之间交互(消息)组成

### 面向过程有什么优缺点?

**优点**:

代码执行效率高

**缺点**:

面向过程程序是一条线下来的，对程序员要求很高，需要程序员详细了解每个功能的细节，这就意味着，不利于合作开发，不利于处理复杂的大型项目

**应用场景**:

需要高效率的场景，比如说操作系统内核OS, 嵌入式开发，算法

### 面向对象程序有什么优缺点?

**优点**:

程序是按照功能模块划分的，对程序员的要求相对较小，不同的程序员负责不同的模块，各个模块之间不需要相互了解, 这样有利于程序员之间合作开发

**缺点**:

思路没有那么清晰，代码会很冗余

最重要的，面向对象程序会花费很多资源来创建对象和管理对象，效率相对较低

### 若类名中涉及到 **class**, 该怎么办?

不要直接写 **class** , 写成 **clazz**

![20210406183934](https://img.fengqigang.cn//img/20210406183934.png)


### What are the different among four access control modifiers?

1. Accessible in the class only(private).

2. Accessible by the world(public).

3. Accessible in the package and all subclasses(protected).

4. Accessible in the package -> the(unfortunate) default. No modifiers are needed.


### What does the keyword `public` means?

Any method in any class can call the method.

### What does the keyword `private` means?

The only methods that can access these instance fields are the methods of the `this` class itself.

### What the access modify should I assign to variable in class?

Variables must explicitly be marked **private**, or they will default to having package access.

If set default to having package access

### If I want to restrict a method to subclasses only or, less commonly, to allow subclass methods to access a superclass field. What can I do?

Declare a class feature as **protected**>

### **public** 访问权限修饰符是什么样的?

**public** 公共的，随便用，大家都能用

![20210406184948](https://img.fengqigang.cn//img/20210406184948.png)

### **默认的，缺省的** 访问权限修饰符是什么样的?

只能在同包下使用, 不同包下不能使用

![20210406185122](https://img.fengqigang.cn//img/20210406185122.png)

### 如果类中没有访问权限，里面的成员是 **public** 可以访问吗?

因为类中没有访问权限，所以里面的成员无法访问

### 如何嵌套定义一个类，它是什么? 有什么特点?

**内部类**

内部类相当于类的成员了，那它立刻就有了四种访问权限

### 使用了访问权限，就一定不可以获取类中的私有成员了吗?

不是，使用反射可以获取一个类中的私有成员

访问权限最重要的的用途是告诉使用者，什么地方出触碰，什么地方不要触碰

### 如何告诉用户这是工具类，是不需要创建对象的?

采取私有化构造方法

![20210406190042](https://img.fengqigang.cn//img/20210406190042.png)

![20210406190631](https://img.fengqigang.cn//img/20210406190631.png)

### 不使用权限控制符，会有什么问题?

1.  没有任何访问权限控制，默认权限，外界可以随便使用
    
2.  成员变量的访问和赋值都是用对象名, 不够细分，如果想对访问或赋值单独操作，没有实现， 比如改变访问结果或者赋值进行修正
    

### 使用正确使用访问权限控制符?

1.  私有化成员变量
    
2.  提供赋值和访问的方法
    

### 使用 **get**, **set** 方法有什么好处?

1.  私有化成员变量, 隐藏实现细节
    
2.  **get**，**set** 方法给私有成员变量，提供了一种访问方式
    
3.  **get**, **set** 方法将成员变量的读、写分离了
    
4.  成员变量的访问从之前的不可控，变为了可控
    

### 封装成员变量后，如何给成员变量赋值?

1.  无参构造方法创建对象
    
2.  有参构造方法
    

### 什么是继承? 如何使用继承?

**继承**:

当需要复用一个类的成员时，引入继承，来实现对成员的复用

**语法**:

\[访问权限修饰符\] class 类名 extends 被继承的类 {}

![20210406191732](https://img.fengqigang.cn//img/20210406191732.png)

### 继承的基本思想是什么? 什么是父类? 什么是子类?

继承的本质是利用代码

**父类(parent class)**：

也称为超类(super class), 基类(base class)

已存在的类，被继承的类，称为父类

**子类**

也称为派生类(derived class), 孩子类(child class)

新创建的类, 继承被继承类的类， 称这为子类

### 父类和子类到底有什么关系呢?

**子类可以看成一个父类，或者说子类 is-a 父类**

1.  代码层面上:

可以用一个父类引用指向一个子类对象，这里其实说明了 **子类就是一个父类对象**

![20210406192806](https://img.fengqigang.cn//img/20210406192806.png)

2.  引用数据类型的定义上:

成员变量 \+ 成员方法， 继承后，子类得到了父类中的所有的成员，现在子类从定义上看，子类有了父类的所有功能，可以当父类用

3.  从逻辑角度上看

- Person
    - Teacher
    - 学生

学生是人，老师也是人，子类就是一个父类

### 子类可以看成父类，那么父类和子类有关系吗?

父类不一定可以看成一个子类，实际上大部分时间都不可以

**子类扩展了父类，多数情况下子类都比父类功能要强大**

### 什么是数据类型的向上转型和向下转型?

父类引用指向子类对象发生了数据类型转换，转换了引用

不需要写代码

**从一个子类的引用转换成了父类的引用**

实现了**向上转型**

同样手动写代码从父类向子类的转化, 就是向下转型


### 使用继承的缺点是什么?

**好处**:

减少了代码冗余，提高了代码的复用性

更有利于功能的扩展，提升可维护性

**弊端**:

父类中对成员进行修改，会体现到每一个子类中，不可选择具体哪个子类生效

### 不同包的子类中访问 **protected** 成员有几种方式?

1.  子类中创建父类对象，然后用父类对象访问
    
2.  子类中创建自身对象，然后访问
    
3.  子类中创建 "兄弟" 类对象，然后访问
    

### 被 **protected** 修饰的成员，其访问权限是什么样的?

1.  同类中，同包中，都可以任意访问(创建父类对象, 子类对象都可以)
    
2.  不同包时候，必须在子类的的那个类中，创建当前子类的对象才可以访问
    

- 创建别的子类对象，不能访问
    
- 创建父类对象，不能访问
    

3.  子类只能在自己的作用范围内访问自己继承的那个父类 **protected** 域

而无法到访问别的子类(同父类的亲兄弟) 所继承的 **protected** 域和父类对象的 **protected** 域

**总结**:

子类继承自父类的 **protected** 成员，必须自己来处理，爸爸帮不了，兄弟姐妹更帮不了

### 将 **protected** 设置复杂，有什么意思?

如果类中某个成员，非常有价值，希望这个成员总是被子类使用，而不会被滥用

1.  使用 **protected** 修饰成员以后，一定能够保证该成员被子类所使用
    
2.  保证子类只能用自己继承的
    

如

**继承财产**

### ![20210406201013](https://img.fengqigang.cn//img/20210406201013.png) 如何访问到这个方法?

```java
Test t = new Test();
```

### ![20210406220313](https://img.fengqigang.cn//img/20210406220313.png) 这里访问clone()可以实现吗?

不行

因为 **clone** 是受保护的，只有在自身类中创建自身对象来访问

```java
Demo d = new Demo();
d.clone();
```

### 什么是单继承，多继承?

**单继承**

一个类有且仅有直接一个父类

### **java** 中有没有多继承?

没有

![20210406220952](https://img.fengqigang.cn//img/20210406220952.png)

### 使用多继承有特点?

1.  支持多继承可就同时获取多个类的成员，这样会更方便
    
2.  当遇到两个类中有同名的成员时会遇到麻烦
    

### 族谱与继承有什么关系(祖先类, 继承层次，继承链)?

**祖先类**:

处在继承上层的类

**继承层次**

由某个祖先派生出来的 **所有类的集合** 叫做继承层次

**继承链**

从某一个子类开始，到其祖先类的路径

![20210406222222](https://img.fengqigang.cn//img/20210406222222.png)

### 父类的私有成员可以继承吗?

可以

父类的私有成员在创建对象后，无法直接调用，看起来像没有继承

但实际上是因为 **没有权限** ，而 **不是没有继承**

![20210406222802](https://img.fengqigang.cn//img/20210406222802.png)

### 如何证明子类继承了私有成员?

![20210406223337](https://img.fengqigang.cn//img/20210406223337.png)

### 父类的构造方法可以继承吗?

构造器不属于成员，并且构造器是给自身类的对象的成员变量赋值用的，也没有必要被继承

### 父类和子类都是需要类加载的，它们的顺序是什么?

先加载父类，再加载子类

### 创建子类对象同时会创建父类对象吗?会在内存中真实创建几个对象?父类成员可能会创建一个对象吗?

显然创建多个对象是不现实的，因为这样代价太高了，如果这么设计堆上应该全是 **Object** 对象

### 在创建S对象(子类)时，其父类成员放在哪里?

子类对象中的父类成员会在子类对象中，开辟一片独有的空间，用来存放这些成员

![20210406224736](https://img.fengqigang.cn//img/20210406224736.png)

### 成员都是有初始化然后再赋值的过程，请问父类的这些成员和子类独有的成员，谁先谁后?

1.  根据常识，先父后子
    
2.  代码现象，子类的成员要依赖于父类的成员赋值，所以父类成员的赋值要在子类之前
    

### 创建对象后，父类成员变量和子类成员变量谁先赋值?

父类先完成赋值，因为子类成员依赖于父类

必须先完成父类成员变量的赋值， 才能保证子类成员变量的赋值正确

### ![20210406225842](https://img.fengqigang.cn//img/20210406225842.png) 其内存图是什么样的?

![20210406225902](https://img.fengqigang.cn//img/20210406225902.png)

