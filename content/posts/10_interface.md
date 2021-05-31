---
title: "10_interface"
date: 2021-04-09T23:09:08+08:00
lastmod: 2021-04-09
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

[toc]

### 子类对象初始化成员变量赋值的顺序是什么样的?

1.  默认初始化, 默认值
    
2.  去找创建子类对象会调用的构造方法，看第一行有没有 **this()**, **super()**, 如果有就去执行，如果没有，默认有 **super()** 仍然去执行
    
3.  肯定要跳到 **父类构造器** ，然后从 **上到下** 执行父类中的 **显示赋值** 和 **构造代码块** ，最后执行父类的构造器
    
4.  如果子类构造器中有 **this**, 回到子类 **this** 构造器. 如果没有 **this**, 直接就回去，从上到下执行子类中的显示赋值和构造代码块，然后执行 **this** 构造器，然后跳到最开始的构造器
    
5.  直接执行该构造器，而不会显式赋值和构造代码块
    

### 如何定义一个接口?

**语法**:

与 **class** 定义一样，接口是和 **class** 同等级别的数据类型

[访问权限修饰符] interface 接口名{}

**All methods of an interface are automatically public**

**Howerver , when implementing the interface, you must declare the method as public, Otherwise the compiler assumes that the method has package access - the default for a class.**

### 接口的命名规范是什么样的?

采取 **大驼峰式** 的

有些程序员，喜欢在接口名的第一个单词之前加一个"I" 用来区分这是一个接口

```java
interface ISpecialSkills{

    public void walkUpright(){
    }
}
```

### 如何在接口中定义方法是怎么规定的?

![20210409135933](https://img.fengqigang.cn//img/20210409135933.png)

接口中的抽象方法不能有方法体

但是可能定义方法

**This particular interface has single method.**

**Some interfaces have multiple methods.**

### 可以在接口中定义中加public abstract 定义方法体吗?

![20210409140240](https://img.fengqigang.cn//img/20210409140240.png)

不可以，默认已经加上了

在接口中的抽象方法，默认都是 **public abstract** 修饰的，这两个关键字无需再加，默认就有

### 接口中有继承的概念吗?

类与接口之间不用继承的概念，用 **实现** 的概念 (implements)

### 接口可以多实现吗?

继承有单继承限制，但是接口不受该限制，接口可以多实现

![20210409140941](https://img.fengqigang.cn//img/20210409140941.png)

### **is-a** 与 **like-a** 有什么区别?

**is-a** 关系的是 **两个类之间的关系** ，如果两个类没有任何实际联系，用继承是不合适的

**like-a** 关系的 **实现强调功能的扩展**， 它不必考虑两个类(接口)之间的实际关系

### 空接口，有什么作用?

一个类实现了一个接口，不管这个接口有没有东西，它都变成了 **这个接口的子类**

### 类与接口有区别吗?

**类**

定义的是一个 **数据集合**，基于这个数据集的一组 **操作(行为)**

类所描述的这一组行为，它们是有关系的(间接) ， 都可以访问同一个数据集合

**接口**

表示数据类型，侧重于描述一组具有 **特殊功能的行为**

这些行为可以完全 **没有任何关系**, 接口中的方法，它们的关系比较的松散

### 接口可以实例化吗?

不可以

![20210409142030](https://img.fengqigang.cn//img/20210409142030.png)

### 接口和继承同时存在时，应该如何定义?

将接口放在继承类后面

![20210409141935](https://img.fengqigang.cn//img/20210409141935.png)

### 为什么接口不可以实例化?

在接口的声明中， 默认有 **abstract**, 接口也是一个抽象的概念，它不能创建实例

这个关键字是可以省略的

### 接口的访问权限是什么?

普遍来说它的访问权限都是 **public** 的，是鼓励去实现接口的，但是 **public** 不是默认的，它的访问权限是可以修改的

### 接口的成员特征是什么样的?

接口中没有 **普通成员变量** 和 **静态成员变量**, 接口的成员变量默认 **public static final** 修饰的全局常量

**普通成员变量**

![20210409191414](https://img.fengqigang.cn//img/20210409191414.png)

**静态成员变量**

![20210409191459](https://img.fengqigang.cn//img/20210409191459.png)

**public static final**

![20210409191617](https://img.fengqigang.cn//img/20210409191617.png)

### 接口中声明全局常量的正确格式是什么样的?

Although you cannot put instance fields in an interface, you can supply constants in them.

Just as methods in an interface are automaically **public**, fields are always **public static final**

![20210409191706](https://img.fengqigang.cn//img/20210409191706.png)

### Can I declare a interface variable?

yeah

```java
Comparable x;
x = new Employee(..);
```

**provided Employee implements Comparable**

### 接口中可以放静态代码块吗?

不可以

虽然接口中的成员变量都是全局常量，但是接口中 **不允许静态代码块** ，所以接口中全局常量 **必须显式赋值**

![20210409191926](https://img.fengqigang.cn//img/20210409191926.png)

### 接口中有普通方法实现吗?

没有，接口中没有普通的方法实现，都是抽象方法， 并且默认是 **public abstract** 修饰的

![20210409192336](https://img.fengqigang.cn//img/20210409192336.png)

### 写接口实现类的格式, 其包名最好怎么取?

需要实现接口的包下, 新建一个包 **impl**

实现类, 类的命名为 **接口名 \+ Impl**

![20210409194221](https://img.fengqigang.cn//img/20210409194221.png)

### 接口中有没有构造方法?

接口中没有构造方法，没有需求，既不能创建对象，以没有成员给子类赋值

![20210409194520](https://img.fengqigang.cn//img/20210409194520.png)

### 接口的子类的特点是什么?

1.  接口的子类如果是一个 **普通类** ，必须 **实现全部抽象方法**
    
2.  接口的子类如果是一个 **抽象类**, 可以 **选择实现一部分**，也可以 **全部都不实现**
    

### 接口的子类可以是一个接口吗?

可以

### 什么样的关系是继承? 什么样的关系是实现?

类与类之间叫 **继承**

接口与接口之间叫 **继承**

类与接口之间叫 **实现**

**继承** 是不能跨越种族的，同种数据类型之间相互继承，**类是单继承的**，**接口是多继承的**

### 接口与接口成员默认是 **public** 还是 **private** 修饰的?

默认都是 **public** 修饰的, 鼓励继承，鼓励重写

### 接口与类之间是什么样的关系?

并列的数据类型

### The `compareTo` method of the `Comparable` interface returns an integer. And, it doesn't work for floating-point numbers, What should I do to solve this problem? Why?

The difference `salary - other.salary` can round to 0 if the salaries are close toether but no identical.

The call `Double.compare(x, y)` simply return -1 if `x < y` or 1 if `x > y`


```java
    @Override
    public int compareTo(Employee other) {
        return Double.compare(salary, other.salary);
    }
```

### A class must do a avail itself of the sorting service -  it must implement a `compareTo` method. But Why can't the `Employee` class simply provide a `compareTo` method without implementing the `Comparable` interface?

The reason for interfaces is that the Java programming languae is strongly typed.

When making a method call, the compiler needs to be able to check that the method actually exist.

Somewhre in the **sort** method will be statements like this:

```java
if (a[i].compareTo(a[j] > 0))
{
	// rearrange a[i] and a[j]
	...
}
```

The compiler must know tha **a[i]** actually has **compareTo** method

If a is an array of **Comparable** objects, then the existence of the method is assured because every class that implements the **Comparable** interface must supply the method.



