---
title: "Day8"
date: 2021-04-07T23:12:51+08:00
lastmod: 2021-04-07
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

Day 8

### 若想限制创建 **Student** 类个数, 其思路是什么?

1. 如果允许外部直接创建对象，显然 **无法控制创建对象的个数**

2. 需要计数器指示外部创建对象的个数

---

### 若想限制创建 **Student** 类个数, 其思路是什么?

1. 如果允许外部直接创建对象，显然 **无法控制创建对象的个数**

2. 需要计数器指示外部创建对象的个数

---

**解决方法**:

1. **私有化构造方法**

2. 提供一个方法来创建对象, 访问权限是 **public**

3. 这个方法必须是 **静态方法**

4. 控制创建对象的计数器，应该是 **静态成员变量** ，被所有对象共享

### 在 **set**, **get**方法怎样赋值比较好( 如width )?

用 **this** 好

![20210407192954](https://img.fengqigang.cn//img/20210407192954.png)

### 如何不希望外界创建数组 **=null** 的对象，应该如何做?

私有化无参构造

![20210407193104](https://img.fengqigang.cn//img/20210407193104.png)

### 在增删改时，如果结果成功或失败了，可以在方法中输出成功或失败的消息吗?

不可以， 输出成功或失败 **不应该** 是在 **增删改** 方法里该做的事情

### 为了防止 **studs** 出现空指针异常， 可以习惯性怎么做?

**判null** 和 **判空**

if (studs == null || studs.length == 0){
	return new Student[0]
}

### 在 **jvm** 中，如何区分 **this** 和 **super** 关键字?

![20210407193708](https://img.fengqigang.cn//img/20210407193708.png)

### 构造代码块时，父类的构造器执行了吗?

构造代码块会在创建对象的时候，**随着构造器执行**

父类的构造器也执行了，并且它 **在子类的构造器之前执行**

所以说，创建子类对象的时候，**隐含了父类构造器的执行**

### 子类对象的初始化方式称为什么?具体是什么样的?

隐式初始化

在子类的每个构造器当中， 如果第一行没有 **this()**, 它都隐含了一个 **super()** 去调用父类的无参构造

### 创建子类对象会调用父类吗?

若第一行没有 **this()** ,

会从隐含 的 **super()** 去调父类的无参构造

### **this()** 与 **super()** 调用构造器都需要在第一行，它们可以共存吗?

不行

因为, 第一行隐含了 **super()** 如果允许不在第一行， 会导致重复给父类成员赋值，显然是错误的

### 所有的类都是直接或间接的继承了 **Object**, **Object** 有没有无参构造?

若 **Object** 中没有构造器， **默认采用无参构造**

![20210407195552](https://img.fengqigang.cn//img/20210407195552.png)

### **super** 和 **this** 有什么区别? 有什么用途?

**区别**:

**this** 表示自己的对象，它不受访问权限控制

**super** 是在子类中表示父类的对象, 受访问权限控制

**用途**:

**this** 可以区分同名的成员变量和局部变量形参

**super** 和 **this** 一起使用可以用来区分父子类中同名的成员(包括方法和变量), 区分的 **前提仍然是访问权限**

### 如何使用 **this** 和 **super** 调用父类和子类的值?![20210407201035](https://img.fengqigang.cn//img/20210407201035.png)

```java
public class supertest {
    public static void main(String[] args) {
        Student st = new Student();

        System.out.println("获取父类a的值");
        st.getSuper();

        System.out.println("获取this类a的值");
        st.getA();
    }
}

class Person {
    int a = 10;
}

class Student extends Person {
    int a = 20;

    public void getSuper() {
        System.out.println(super.a);
    }

    public void getA() {
        System.out.println(this.a);
    }
}
```

![20210407201117](https://img.fengqigang.cn//img/20210407201117.png)

### 父子类中可以出现同名的变量吗?

可以

![20210407201401](https://img.fengqigang.cn//img/20210407201401.png)

### ![20210407201457](https://img.fengqigang.cn//img/20210407201457.png)输出的是20, 这个a是被覆盖掉了，还是因为某些原因没有覆盖但是访问不到, 如何证明?

```java
public class supertest {
    public static void main(String[] args) {
        Student st = new Student();

        System.out.println("获取父类a的值");
        st.getSuper();

        System.out.println("获取this类a的值");
        st.getA();
    }
}

class Person {
    int a = 10;
}

class Student extends Person {
    int a = 20;

    public void getSuper() {
        System.out.println(super.a);
    }

    public void getA() {
        System.out.println(this.a);
    }
}
```

![20210407202027](https://img.fengqigang.cn//img/20210407202027.png)

a 不是被覆盖掉了, **仍然可以去访问它**

使用对象名点成员变量的方式访问变量时，**编译器** 存在一个 **检索机制**

它首先会去从引用所在的那个类中去找这个成员变量

如果这个引用找不到，就去父类中找，找完所有的父类，直到 **Object**， 都找不到，它会编译报错

### 当引用数据类型与它的具体类型不一样时，会根据什么来决定它的最终取值?

根据引用的类型来取值


```java
public class supertest {
    public static void main(String[] args) {
        Father f = new Son();
        System.out.println(f.a);
    }
}

class Father {
    int a = 10;
    int b = 100;

    public int getFatherA() {
        return a;
    }
}

class Son extends Father {
    int a = 20;

    public int getSonA() {
        return a;
    }
}
```

![20210407203426](https://img.fengqigang.cn//img/20210407203426.png)

### 成员变量隐藏的原理是什么样的?

当使用对象名点成员变量的方式访问变量时，编译器存在一个检索机制，会首先从引用所有的那个类中去找这个成员变量

如果这个引用找不到，就去父类中找，找完所有的父类，直到 **Object**, 都找到，它会编译报错

因为这种检索机制父子类中同名的成员变量就找到不父类中去了，父类的成员被隐藏了

对象名点访问成员变量，在编译时期就能够确定它访问的是哪个类的成员变量，就是那个 **引用的类**

### 静态成员变量可以被子类继承吗?

可以

```java
public class supertest {
    public static void main(String[] args) {
        System.out.println(B.a);
    }
}

class A{
    static int a = 10;
}

class B extends A {
}
```
![20210407204108](https://img.fengqigang.cn//img/20210407204108.png)

### 父子类中同名的静态成员变量， 它们之间有什么关系? 覆盖了还是隐藏又或者是其他的了?

静态的成员 **不属于对象**， 而我们讨论继承的时候，一般都是说对象的继承，对象和静态成员没有关系

所以静态成员不要用继承去讨论，不同类的静态成员完全是独立的，它们 **不存在隐藏或者覆盖** 这种关系

```java
public class supertest {
    public static void main(String[] args) {
        System.out.println(B.a);
    }
}

class A{
    static int a = 10;
}

class B extends A {
}
```

![20210407205018](https://img.fengqigang.cn//img/20210407205018.png)

### 若继承中有静态成员的需求，可以采用什么样的方法去访问父类的静态成员?

采用子类的类名访问静态成员

```java
public class supertest {
    public static void main(String[] args) {
        System.out.println(B.a);
        B.a = 888;
        System.out.println(B.a);
        System.out.println(A.a);
    }
}

class A {
    static int a = 10;
}

class B extends A {
    static int a = 100;
}
```

![20210407205421](https://img.fengqigang.cn//img/20210407205421.png)

### 父子类能否出现同名的方法?

可以

![20210407205606](https://img.fengqigang.cn//img/20210407205606.png)

### 创建子类对象，并用子类的引用指向对象，调用方法, 它的访问结果是什么? ![20210407210207](https://img.fengqigang.cn//img/20210407210207.png)

![20210407210226](https://img.fengqigang.cn//img/20210407210226.png)

方法被覆盖了

用对象名点方法名编译器同样有类似的 **检索机制**: 

先从引用的类型中去找，找不到, 从父类中找，直到完全找不到, 再报错

**原因**:

对象名点方法名编译器同样有类似的检索机制:

先从引用的类型中去找，找不到, 从父类中找，直到完全找不到报错

这种检索机制导致引用类型中有的成员方法 才能被调用

编译器在检索时，只能知道变量的类型，在编译时期，如果想要通过编译，所访问的成员，必须是这个类型中有的

### 在方法的覆盖原理中，方法的最终执行结果，是由什么所决定的?

方法的最终执行结果，不是在编译时期决定的，而是程序运行起来以后，根据引用所指向的实际类型决定的

如果有同名的方法，因为方法被覆盖掉了，所以显示出子类的一个特征

![20210407211155](https://img.fengqigang.cn//img/20210407211155.png)

### @Override 注解是什么样的? 如何使用?

两个父子类之间发生方法的重写后，可以用一个注解指示被覆盖的方法

@Override 注解

这个注解可以检查 两方法之间是否发生了方法重写，如果不是方法重写, 会报错

![20210407211514](https://img.fengqigang.cn//img/20210407211514.png)

### 若要进行方法重写，需要注意什么?

不必要完全一模一样，但是肯定是有限制的

**注意**

重写的方法 **访问权限** 必须 **大于等于** 原方法，要比父类的方法的访问权限更 **松**

父类的私有方法 

**没有权限访问，不能够发生方法重写**

### 如果方法覆盖了，可以访问被覆盖的方法吗?![20210407213009](https://img.fengqigang.cn//img/20210407213009.png)

**super** 关键字可以用来区分子类同名

```java
public class supertest {
    public static void main(String[] args) {
        Cat c = new Cat();
        c.test();
        c.invokeSonTest();
        c.invokeSonTest2();
        c.invokeFatherTest2();
    }
}

class Animal {
    public void test() {
        System.out.println("Animal");
    }
}

class Cat extends Animal {
    @Override
    public void test() {
        System.out.println("Cat");
    }

    public void invokeSonTest() {test();}
    public void invokeSonTest2() {this.test();}
    public void invokeFatherTest2() {super.test();}
}
```

![20210407213059](https://img.fengqigang.cn//img/20210407213059.png)


### 静态方法可以继承和重写吗?

子类 **可以继承** 父类的静态成员方法

如果同名了，不是方法的重写，它们是独立的两个方法, 只不过凑巧同名了

静态方法 **不能重写**

```java
public class supertest {
    public static void main(String[] args) {
        A.test();
        B.test();
    }
}

class A {
    static void test() {
        System.out.println("A");
    }
}

class B extends A {
    static void test() {
        System.out.println("B");
    }
}
```

![20210407213636](https://img.fengqigang.cn//img/20210407213636.png)

### 什么是 **final** 关键字?

**final** 修饰类表示最终的类，表示一个不能被继承的类

**final** 修饰类时，放在访问权限修饰符和class之间，表示该类无法被继承

![20210407214140](https://img.fengqigang.cn//img/20210407214140.png)

### 什么时候用 **final** 来修饰类?

1. 不需要复用成员

2. 功能已经特别强大， 足够满足需求

3. 需要绝对保证安全，以致于不让它被继承

**常见的final类**

- String

- System

- Math

### 用 **final** 来修饰的类可以继承和重写吗?

**final** 应该放在访问权限修饰符的后面，返回值的前面

**final** 修饰的方法无法被重写，但是可以被继承

```java
public class supertest {
    public static void main(String[] args) {
    }
}

class A {
    public final void test() {
    }
}

class B extends A {
    @Override
    public void test() {
    }
}
```

'test()' cannot override 'test()' in 'com.feng.A'; overridden method is final

### **final** 修饰的变量， 最终表示的是什么?

表示最终的变量，表示一个常量

### 常量的分类是什么样的?

**字面值常量**

"hello world!"

10 

true

null

**自定义常量**

用 **final** 修饰的变量就是自定义的常量

### **final** 修饰一个成员变量会怎样?

它只是让这个变量的取值无法改变，但是在内存中的位置不变

### **final** 修饰一个基本数据类型的变量会怎样?

表示这个基本类型的变量取值无法改变

### **final** 修饰一个引用数据类型的变量会怎样?

表示引用是一个常量时，表示地址不变了，也就是指向的对象不变了，对象的属性(状态)仍然可以改变

### 在方法中有哪些地方有局部变量?

1. 方法体中

2. 形参列表

### 用 **final** 修饰方法体中的局部变量会怎样?

表示定义了一个局部的常量，意味着，方法的后面就不能修改它的取值了

如果只声明了一个局部常量，那么可以赋值一次，后面就无法再赋值了

![20210407233711](https://img.fengqigang.cn//img/20210407233711.png)

### 用 **final** 修饰形参列表，会怎么样?

表示的是传入的参数已经成为一个常量了，无法修改

![20210407233913](https://img.fengqigang.cn//img/20210407233913.png)

### **final**修饰成员变量哪些要求?

1. 显示赋值

2. 构造代码块

3. 构造器

以上三种方法，选择一种即可，介是也仅仅只能用一种，因为赋值一次，之后不能修改了

![20210407234119](https://img.fengqigang.cn//img/20210407234119.png)

### ![20210407234152](https://img.fengqigang.cn//img/20210407234152.png) 加上无参的构造方法，会不会报错?

会，因为无参构造不能保证每个对象都能给常量赋值

### 用 **final** 修饰 静态成员变量是什么?

**final**修饰静态成员变量是全局常量

### **final** 修饰的变量，其命名规范是什么?

字母全部大写，每个单词之间用下划线("_")

如

MY_AGE = 18

MY_NAME = 长风

### **final** 在哪些时候可以修饰静态成员变量?

静态成员变量的赋值方式：

**类加载时期**：

1. 显式赋值

2. 静态代码块

**创建对象时期**: (创建对象时，早已经触发类加载了)

1. 构造代码块

2. 构造器

### 是用 **final static** 还是 **static final** 好?

建议用 **static final**

### 访问 **final** 修饰的成员变量会触发类加载吗?

1. 如果该全局常量是 **基本数据类型**， **不会触发类加载**

2. 如果该全局常量是 **引用数据类型**, **不一定会触发**

- **String** 如果用 **字面值常量** 直接赋值的，**不会触发类加载**

- **String** 如果是 **用构造器** 创建的对象，**会触发类加载**

- 如果是除了 **String** 之外的 **自定义类**，**会触发类加载**

### 如何用 **final** 修饰引用数据数据?会出现什么情况?

```java
public class FinalTest {
    public static void main(String[] args) {
        final C c = new C();
        c.a = 10;
    }
}

class C {
    int a = 10;
}
```

表示该引用已经成为一个常量了，它里面的地址不能再改变了

### **final** 修饰匿名对象可以吗?

不可以，不合法

```java
public class FinalTest {
    public static void main(String[] args) {
        final new C();
    }
}

class C {
    int a = 10;
}
```

![20210408091939](https://img.fengqigang.cn//img/20210408091939.png)

### 什么是多态?

同一个事物，在不同的情况下，表现出不同的行为

在 **java** 面向对象当中， 多态指的是:

- 同一个事物: **同一个引用**

- 不同的情况: **引用指向不同(实际对象)**

- 不同行为: **不同的方法结果**

### 多态发生的条件是什么?

1. 需要继承，父子类

2. 需要方法的重写

3. 需要父类引用指向(不同的)子类对象

### ![20210408140637](https://img.fengqigang.cn//img/20210408140637.png) 如何实现其多态访问?

**父类引用指向(不同的)子类对象**

```java
public class Demo {
    public static void main(String[] args) {
        Phone p;
        p = new ApplePhone();
        p.call();
        p = new SamsungPhone();
        p.call();
        System.out.println(p.price);
    }
}

class Phone {
    double price;
    public void call() {
        System.out.println("手机都能打电话");
    }
}

class ApplePhone extends Phone {
    @Override
    public void call() {
        System.out.println("hi siri");
    }
}

class SamsungPhone extends Phone {
    @Override
    public void call() {
        System.out.println("炸了");
    }
}
```

### 什么情况下不能使用多态?

1. 不能继承， **final** 修饰的类

2. 不能被重写的方法

**final** , **private**, **static** , 构造方法

3. 写代码，如何不按照类引用指向(不同的)子类对象，也没有多态

### 成员变量中有没有多态现象?

多态指的是:

有父类引用指向子类对象，多态是指方法的重写，**与成员变量无关**

### 多态时(无论多不多态都是一样的), 成员变量的访问特征是什么样的?

1. 编译时，**看左边**，左边是什么类型就意味着可以访问这个类型中有的成员变量 

2. 运行时 **看左边** ，编译时期就已经确定它取谁的值了，取左边引用类中成员的值

### 方法中有没有多态现象?

有， 但是有条件，必须是重写了继承父类的方法

### 多态中的方法访问特征(检索机制和访问机制)是什么样的?

1. 编译时 **看左边**， 意味着引用类型中没有的方法，不能被调用

2. 运行时 **看右边**， 意味着方法的结果表现出引用所指向的实际类型

### 多态的优缺点是什么?

**优点**:

1. 要实现多态，必须要继承，提高了程序的可维护性性

2. 发生多态后，同一个引用调用方法产生不同的行为, 提高了程序的简洁性和扩展性

**缺点**

1. 父类的引用指向子类对象，就无法访问子类独有的行为，必须要做强制类型转换




 





