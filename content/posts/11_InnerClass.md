---
title: "11_InnerClass"
date: 2021-04-10T22:36:59+08:00
lastmod: 2021-04-10
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 什么是内部类?

嵌套定义在 **一个类的内部** 的类

### 内部类有什么用?

1.  封装

![20210409203437](https://img.fengqigang.cn//img/20210409203437.png)

私有化 **CPU** 这个类后，就不能在 **Computer** 外部访问这个类了

2.  内部类互相访问

两个独立的类之间受访问权限限制，而当一个类进入另一个类内部成为内部类就不再受访问权限限制了，可以互相访问私有成员

### 内部类如何分类? (成员位置， 局部位置)

**定义在成员位置**

1.  成员内部类
    
2.  普通成员内部类
    
3.  静态内部类
    

**定义在局部内部类**

1.  匿名局部内部类
    
2.  lambda
    

### 什么是成员内部类?其定义是什么?

**成员内部类**

最普通的内部类， 它定义在另一个类的成员位置，可以看成该类的一个成员

**语法**

```java
[访问权限修饰符] class EnclosedClazz{
[访问权限修饰符] class InnerClazz{
}
}
```

### 普通的类有几种访问权限修饰符?

两种，没有 **protected** , **private**

class 是用来被实例化的，所以只有 **默认** 和 **public** 访问权限修饰符

### 成员内部类的访问权限修饰符有哪些?

成员内部类相当于外围类的成员了，有4种访问权限

**public** , **protected** , 默认， **private**

其中 **private** 最为常见

### 什么是类加载? 类加载时机有哪些?

**类加载**:

是一种懒加载，用到的时候才加载，不得不加载才加载

**时机**

1.  new 对象
    
2.  执行 main 方法
    
3.  访问类的静态成员
    
4.  子类类加载触发父类类加载, 并且在子类之前
    

### 成员内部类的类加载情况有哪些?

创建内部类对象

成员内部类想创建对象，**必须依赖于外围类**，在外围类对象的基础上，才能创建成员内部类对象

### 成员内部类中可以有普通成员变量，静态成员变量，全局变量吗?

1.  可以有普通成员变量
    
2.  不能有静态成员变量
    
3.  可以有全局常量, 但是那些会触发类加载的全局常量不能有
    

**普通成员变量与静态成员变量**

![20210409205101](https://img.fengqigang.cn//img/20210409205101.png)

**全局常量**

![20210409205253](https://img.fengqigang.cn//img/20210409205253.png)

**内部类只有依赖于外围类来触发类加载, 其他都不行**

### 成员内部类中成员方法特点是什么样的?

1.  可以 **有普通成员方法**
    
2.  **没有静态成员方法**
    

**静态成员方法会触发类加载**

### 成员内部类中有没有构造器和代码块?

**构造器**

必须有，需要创建对象，需要给成员变量赋值

**代码块**

静态代码块 **没有**

构造代码块有

### 成员内部类与外围类相互依赖而存在吗?

不是

成员内部类对象 **依赖于** 外围类对象而存在

外围类对象 **并不依赖于** 成员内部类对象

### 外部的类可以继承内部类吗?

可以

### 成员内部类有什么特点?

1.  成员内部类和外围类是亲兄弟，自己人，它们之间的访问 **不受访问权限限制， 即便私有的，它们也可以互相访问**
    
2.  成员内部类的对象 **依赖于外围类对象** 而存在
    

### 成员内部类的成员方法中，有没有外围类对象?

有， 有外围类对象才能有内部类对象，内部类对象存在了，外围类对象必然存在

### 外围类的成员方法中，有没有成员内部类对象?

没有， 外围类对象和内部类对象没有依赖关系，如果想有，需要手动创建

### 若成员内部类中和外围类成员有同名，怎么办?

**普通成员变量同名**

1.  什么都不加，就近原则，优先选择内部类自身的成员
    
2.  可以用 **this** , 表示内部类自身的成员
    
3.  内部类的成员方法中必然有外围类对象，也有一个引用指向它，作类一个隐藏的传参，用 **外围类的类名.this** 表示
    

### 如果成员内部类中静态成员变量同名怎么办?

成员内部类中 **没有静态成员变量**

### 如果成员内部类中全局常量同名怎么办?

用类名去区分

### 什么是静态内部类?

在一个成员内部类基础上，加一个 **static** 修饰即可

静态内部类也是处在 **外围类** 成员位置的内部类, 不同的是它需要使用 **static** 修饰

### 如何定义一个静态内部类?

```java
[访问权限修饰符] class EnclosedClazz {
    [访问权限修饰符] static class InnerClazz {
    }
}
```

![20210410155531](https://img.fengqigang.cn//img/20210410155531.png)

### 静态内部类的外围(普通)类的访问权限修饰符有哪些?

**public** 和 缺省的

![20210410155821](https://img.fengqigang.cn//img/20210410155821.png)

![20210410155839](https://img.fengqigang.cn//img/20210410155839.png)

### 内部类的访问权限修饰符有哪些?

4种

**public**, **private**, 缺省的, **protected**

![20210410155946](https://img.fengqigang.cn//img/20210410155946.png)

![20210410160005](https://img.fengqigang.cn//img/20210410160005.png)

![20210410160054](https://img.fengqigang.cn//img/20210410160054.png)

![20210410160155](https://img.fengqigang.cn//img/20210410160155.png)

### 静态内部类是外围类的静态成员吗?

**不是**

其实两个类没有太大关系

静态内部类和外围类没有依赖关系，实际上它完全可以脱离外围类，独立的自己做一个类

### 静态内部类可以独立做类，它的成员和普通类有什么区别?

它的成员和普通类没有区别

![20210410160717](https://img.fengqigang.cn//img/20210410160717.png)

### 静态内部类可以继承 **普通类** 吗和 **静态类** 吗?

不可以继承 **普通类**

可以继承 **静态类**

![20210410161201](https://img.fengqigang.cn//img/20210410161201.png)

![20210410161021](https://img.fengqigang.cn//img/20210410161021.png)

### 静态内部类什么时候类加载? 静态内部类类加载需不需要依赖外围类?如何证明?

静态内部类和外围类没有依赖关系，实际上它完全可以脱离外围类，独立的自己做一个类

**静态内部类的加载不需要依赖外围类**

![20210410161647](https://img.fengqigang.cn//img/20210410161647.png)

### 静态内部类的成员方法中，有没有外围类对象?

**静态内部类与外围类互相不影响**

静态内部类中 **没有** 外围类对象

### 外围类对象的成员方法中，有没有静态内部类?

**静态内部类与外围类互相不影响**

外围类对象中 **没有** 静态内部类

### 静态内部类访问外围类有什么特点?

需要**创建对象**, 除了不受访问权限限制， 其它的和普通类访问一样

```java
public class Demo { //外部类
    public static void main(String[] args) {
        EnclosedClazz.Inner inner = new EnclosedClazz.Inner();
        inner.test();
    }
}

class EnclosedClazz { //外围类
    int a = 10;
    private int b = 20;
    static int c = 30;
    static final int D = 40;

    static class Inner {
        int a = 100;
        private int b = 200;
        static int c = 300;
        static final int D = 400;

        public void test() {
            EnclosedClazz ec = new EnclosedClazz();
            System.out.println(ec.a);
            System.out.println(ec.b);
            System.out.println(EnclosedClazz.c);
            System.out.println(EnclosedClazz.D);
            System.out.println(this.a);
        }
    }
}
```

![20210410162954](https://img.fengqigang.cn//img/20210410162954.png)

### 外围类访问静态内部类成员有什么特点?

需要**创建对象**, 除了不受访问权限限制， 其它的和普通类访问一样

### 外部类访问静态内部类成员有什么特点?

直接创建静态内部类对象， **受访问权限限制**

创建对象以后,访问成员，**也受访问权限限制**

### 静态内部类访问外部类成员有什么特点?

直接创建外部类对象，**受访问权限限制**

### ![20210410163851](https://img.fengqigang.cn//img/20210410163851.png)其答案是什么?

![20210410163945](https://img.fengqigang.cn//img/20210410163945.png)

### 什么是局部内部类?

定义在 **一个方法或者一个作用域** 里面的类

将局部内部类看成是 **局部变量** 即可

![20210410164800](https://img.fengqigang.cn//img/20210410164800.png)

### 局部内部类有没有访问权限修饰符?

没有， **方法的作用域已经限制** 了这个局部内部类，**无需访问权限再限制**

![20210410165023](https://img.fengqigang.cn//img/20210410165023.png)

### 局部内部类有没有 **static** 修饰符?

没有, 局部变量不需要 **static** 修饰

![20210410165209](https://img.fengqigang.cn//img/20210410165209.png)

### 局部内部类的类加载时机有哪些?

1.  调用外面的方法
    
2.  在方法中创建这个局部内部类的对象
    

![20210410165356](https://img.fengqigang.cn//img/20210410165356.png)

### 在方法体中创建局部内部类的对象应该写在哪里![20210410165603](https://img.fengqigang.cn//img/20210410165603.png)? 1处还是2处?

**2处**, 在方法中，局部内部类的声明 **下面创建对象**

### 局部内部类的成员特点是什么样的?

和成员内部类一样，没有静态成员，有全局常量

![20210410165921](https://img.fengqigang.cn//img/20210410165921.png)

### 局部内部类定义在哪里?

局部位置

### 什么时候用局部内部类?

当在局部位置，碰到了一个麻烦的问题，需要使用类来解决

但是又 **不希望这个类被外界知道** ，这种情况需要使用局部内部类

### 可以在外部类中创建局部内部类对象吗?

不可以

### ![20210410170805](https://img.fengqigang.cn//img/20210410170805.png) 调用这方法的思路是什么?(土办法调用)?

1.  新建一个 **class**, 这个 **class** 中有 **method** 方法
    
2.  **class** 是一个接口的实现, 接口中有 **method**, **class** 改写 **method** 接口
    
3.  **class** 是 **接口** 的子类
    

```java
public class Demo {
    public static void main(String[] args) {
        test(new IAImpl());
    }

    public static void test(IA a) {
        a.method();
    }
}

interface IA {
    void method();
}

class IAImpl implements IA {
    @Override
    public void method() {
        System.out.println("土办法调用test()方法");
    }
}
```

![20210410171522](https://img.fengqigang.cn//img/20210410171522.png)

### ![20210410170805](https://img.fengqigang.cn//img/20210410170805.png) 调用这方法的思路是什么(如何采用内部类的方式实现)?

1.  如果一个方法需要传入接口或抽象类，应该 **传它们的子类对象**
    
2.  如果一个方法需要返回接口或抽象类，应该 **返回它们的子类对象**
    

```java
public class Demo {
    public static void main(String[] args) {
        test(test2());
    }

    public static void test(IA a) {
        a.method();
    }

    public static IA test2() {
        class IAImpl implements IA {
            @Override
            public void method() {
                System.out.println("高端的调用test()方法 ");
            }
        }
        return new IAImpl();
    }


}

interface IA {
    void method();
}
```

![20210410173042](https://img.fengqigang.cn//img/20210410173042.png)

### ![20210410173421](https://img.fengqigang.cn//img/20210410173421.png) 如何输出这三个 **num** ?

Outer需要创建对象， 所以需要Outer().new

```java
public class Demo {
    public static void main(String[] args) {
        Outer.Inner inner = new Outer().new Inner();
        inner.show();
    }
}

class Outer {
    public int num = 10;
    class Inner {
        public int num = 20;
        public void show() {
            int num = 30;
            System.out.println(num);
            System.out.println(this.num);
            System.out.println(Outer.this.num);
        }
    }
}
```

![20210410173744](https://img.fengqigang.cn//img/20210410173744.png)

