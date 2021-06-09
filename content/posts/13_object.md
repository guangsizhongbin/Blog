---
title: "13_object"
date: 2021-04-13T21:42:49+08:00
lastmod: 2021-04-13
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 什么是 **API** ?

Application Programming Interface(API)

应用程序编程接口，在**Java** 当中指的是一些先定义好的类和方法

**作用**

开发者可以在不关注具体实现细节的前提下，使用和这些已经预先定义好的类和方法实现自己的需求

### **Object** 类有什么特点?

1.  **Object** 类所有类继承层次的祖先类, 所有类(包括数组)都 **直接或间接的继承** 自该类，都实现了该类的方法
    
2.  在自定义类时，并不需要特别标注 **extends Object**
    
3.  如果一个类没有明确的的指出它的父类，**Object** 类就默认被认为是这个类的父类，**extends Object** 则被省略了
    

### 为什么所有类都有一个默认无参?

1.  当一个类没有定义构造方法的时候，就会自动添加默认构造方法
    
2.  一旦有默认构造方法，在创建子类对象的时候，就会执行子类对象的隐匿初始化
    
3.  隐式初始化，默认调用父类的无参构造
    
4.  最终，一定能保证，调用到 **Object** 类的无参构造方法，先初始化 **Object** 这个父类
    

### ![20210412140548](https://img.fengqigang.cn//img/20210412140548.png)为什么不能访问 **clone** 方法

**clone** 方法是 **protect** 修饰的， 只能在自己的子类中访问

### 方法声明中 **public final Class&lt;?&gt; getClass()** 分别代表什么意思?

1.  **public** 访问权限，调用时不必考虑权限问题
    
2.  **final** 该方法可以被继承但是不能被重写
    
3.  **Class** 返回值类型， **Class** 是大写的 **class** , 它表示一个类，说明该方法的返回值是 **Class 对象** 表示泛型
    
4.  **getClass** 是方法名 () 表示方法不需要参数
    

### **Class** 对象是什么对象? Class类是什么类?

**Class 对象** 是该类的运行时对象

![20210412141242](https://img.fengqigang.cn//img/20210412141242.png)

### **Class 对象** 与 该类的对象有区别吗?

有

![20210412141319](https://img.fengqigang.cn//img/20210412141319.png)

### ![20210412142226](https://img.fengqigang.cn//img/20210412142226.png) 如何判断这两个类是否是相同的 **Class对象**?

![20210412142351](https://img.fengqigang.cn//img/20210412142351.png)

![20210412142359](https://img.fengqigang.cn//img/20210412142359.png)

**不同的类，运行不同的Class对象**

### ![20210412142518](https://img.fengqigang.cn//img/20210412142518.png) 它们是相等的吗?为什么?

![20210412142547](https://img.fengqigang.cn//img/20210412142547.png)

同一个类运行时的 **class** 对象是唯一的

### **运行时对象** 和 **类的对象** 有什么区别?

**运行时对象**

也叫类对象，整个程序运行期间独一份，不可能有两个

**类对象**

想创建几个就有几个

### **getName()** 与 **getSimpleName()** 如何使用?

**getSimpleName**

Return the simple (unqualified) name of this element.

**getName**

Get the name of the category of which this attribute value is an instance

这两个方法都是 **Class** 方法

需要用 **getClass()** 先获取 **Class**

然后用 **Class** 获取 **getName**, **getSimpleName**

```java
public class Demo {
    public static void main(String[] args) {
        Student s = new Student();
        Class clClazz = s.getClass();

        System.out.println(clClazz.getName());
        System.out.println(clClazz.getSimpleName());
    }
}

class Student {
}
```

![20210412202502](https://img.fengqigang.cn//img/20210412202502.png)

### **public String toString()** 是什么意思?

访问权限不用考虑

返回值是一个字符串

不需要任何参数

**It is recommended that all subclasses override this method**

### ![20210412202913](https://img.fengqigang.cn//img/20210412202913.png) 是什么意思?

return getClass().getName() + "@" + Integer.toHexString(hashCode());

**getClass().getName()** 一个类的全限定类名 \+ "@"

**Interger.toHexString(hashCode())**

返回对象的十六进制的地址值

### ![20210412203656](https://img.fengqigang.cn//img/20210412203656.png) 会输出什么?

return getClass().getName() + "@" + Integer.toHexString(hashCode());

一个类的全限定类名 \+ @ \+ 对象的十六进制的地址值

![20210412203709](https://img.fengqigang.cn//img/20210412203709.png)

### 如何改写 **toString()** , 在哪里?

在对应的类中必写 **toString()**

![20210412204034](https://img.fengqigang.cn//img/20210412204034.png)

### **public boolean equal(Object obj)** 是什么意思?

首先不用关心访问权限

返回值的类型是 **boolean** , 要么是 **true** , 要么是 **false**

意味着所有的类的对象都可以传入

### What are the Java Language Specification requires that the `equals` method have properites?

1. reflexive

For any non-null reference `x`, `x.equals(x)` should return `true`.

2. symmetric

For any references `x` and `y`, `x.equals(y)` should return `true` if and only if `y.equals(x)` return `true`.

3. transitive

For any references `x`, `y` and `z` , if x.equals(y) return `true` and `y.equals(z)` return true, then `x.equals(z)` should return `true`.

4. consistent

If the objects to which `x` and `y` refer haven't changed, then repeated calls to `x.equals(y)` return the same value.

5.  non-null 

For any non-null reference `x`, `x.equals(null)` should return `false`.

### How to write the perfect `equals` method?

1. Name the explicit parameter `otherObject`

2. Test whether `this` happens to be identical to `otherObject`

```java
if (this == otherObject) return true;
```

3. Test whether `otherObject` is `null` and return `false` if it is.

```java
if (otherObject == null) return false;
```

4. Compare the classes of `this` and `otherObject`

- **subclasses**

```java
if (getClass() != otherObject.getClass()) return false;
```

- **all subclasses**

```java
if (!(otherObject instanceof ClassName)) return false;
```

5. Cast `otherObject` to a variable of class type

```java
ClassName other = (ClassName) otherObject
```

6. Compare the fields, as required by notion of equality

```java
return field1 == other.field1;
```


### 如何判断对称性? **y.equal(x)** 返回 true 时， **x.equal(y)** 也应返回 **true**

使用成员变量的取值来判断对象相等，这一条就会自动满足，因为成员变量的取值就是一个值，数学意义上肯定满足对称性

### 如何在重写 **equals** 中满足 **自反性** ?

**判断它是否是同一个对象**

**x.equals(obj)**

```java
public boolean equals(Object obj){
    if (this == obj){
        return true;
    }
}
```

### 什么是 **BigDecimal** 类?

**Immutable, arbitrary-precision signed decimal numbers**

### 如何用 **BigDecimal** 实现 **1 - 0.9** ?

public BigDecimal substract (BigDecimal subtrahend)

Returns a BigDecimal whose value is (this - subtrahend), and whose scale is max(this.scale(), subtrahend.scale())

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println(1 - 0.9);
        BigDecimal b1 = new BigDecimal("1");
        BigDecimal b2 = new BigDecimal("0.9");
        BigDecimal b3 = b1.subtract(b2);
        System.out.println(b3);
    }
}
```

![20210412213715](https://img.fengqigang.cn//img/20210412213715.png)

### 若在 **equals** 方法中允许子类对象来比较是否相等, 该如何实现排他性?

就不能用 **getClass()** 方法了，需要使用 **instanceof** 做类型判断

因为 **instanceof** 允许传入子类对象，而不仅仅是它自身的对象

![20210412214238](https://img.fengqigang.cn//img/20210412214238.png)

### **public int hashCode()** 是什么意思?

返回该对象的哈希码值，方法返回的 **int** 结果就是哈希码值

### What is a `native` method?

If a method is a `native` method, not implementd in the Java programming language.

Native methods can bypass the access control mechanisms of the Java language.

### **public native int hashCode()** 中的 **native** 是什么意思?

**native** 方法:

特指那些 **java** 代码中去调用 **C/C++** 实现的方法，本地方法虽然不是抽象方法，但是, 不是**java**实现的方法

### 如何用 **hashCode** 判断两个 Teacher 对象是否相等?

```java
public class Demo {
    public static void main(String[] args) {
        Teacher t1 = new Teacher(19, "张三", 1000);
        Teacher t2 = new Teacher(19, "张三", 1000);
        System.out.println(t1.hashCode() == t2.hashCode());
    }
}

class Teacher {
    int age;
    String name;
    int salary;

    public Teacher() {
    }

    public Teacher(int age, String name, int salary) {
        this.age = age;
        this.name = name;
        this.salary = salary;
    }
}
```

![20210412215125](https://img.fengqigang.cn//img/20210412215125.png)

### **equals** 方法 与 **hashCode** 方法有什么应用?

集合当中会优先调用 **equals** 方法用来比较两对象是否相等，如何相等，它就不会输入集合

但是如何 **equals** 方法认为对象相等， 但是 **hashCode()** 方法返回值却不同，就会导致一个认为不应该存，一个认为应该存的情况发生， 这显然是不合理的

**equals** 方法如果重写， 就必须重写 **hashCode** 方法

### **protected void finalize() throws Throwable {}** 是什么意思?

**protected** 不同包下必须在子类中创建子类自身对象才能够访问

**void** 方法没有返回值

**throws Throwable** 抛出异常

### **protected void finalize() throws Throwable {}** 中的 **{ }** 方法体是空的，这个方法有什么意义?

这种空的方法，然后又是 **protected** 权限， 是为了保证子类自由的重写该方法，并且保证该方法不会被子类外的其他类滥用

### 空接口有什么用?

一个类实现了某个接口，并不仅仅是简单的继承成员，更重要的它数据类型发生了变化，**它成为了接口的实现子类**

可以用 **instanceof** 关键字进行判断该引用指向的对象是否是接口的实现类对象

```java
public class Demo {
    public static void main(String[] args) {
        A a = new A();
        if (a instanceof IEmptyInterface) {
            System.out.println("A实现了空接口，程序正常执行");
        } else {
            System.out.println("报错，抛出异常");
        }
    }
}

class A implements IEmptyInterface {
}

interface IEmptyInterface {
}
```

![20210412221737](https://img.fengqigang.cn//img/20210412221737.png)

### Can I have to write that `public class Employee extends Object`?

NO

The ultimate superclass **Object** is taken for granted if no superclass is explicitly mentioned.

### Where is the `hash code` come from?

A `hash code` is an integer that is derived from an object.

The `hashCode` method is defined in the `Object` class.

Therefore, every object has a default hash code.

That hash code is derived from `the object's memory address.


