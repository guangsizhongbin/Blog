---
title: "Spring01"
date: 2021-06-24T23:51:14+08:00
lastmod: 2021-06-24
author: "xiaonan"
math:
 enable: true

tags: [spring]
categories: [王道]
---

01_Spring


### 单例模式


**构造方法后没有;**

**public class 后没有()**

#### 线程不安全的单例模式

高并发下并不安全

```java
public class TestSigteon {
    static TestSigteon testSigteon;
    private TestSigteon(){}

    public static TestSigteon getSigteonInstance(){
        if(testSigteon == null){
            testSigteon =  new TestSigteon();
        }
        return testSigteon;
    }
}
```

#### 线程安全的单例模式

将 `synchronized` 放在 `public` 与 `static` 之间

```java
public class TestSigteon {
    static TestSigteon testSigteon;
    private TestSigteon(){}

    public synchronized static TestSigteon getSigteonInstance(){
        if(testSigteon == null){
            testSigteon =  new TestSigteon();
        }
        return testSigteon;
    }
}
```

#### 什么是懒加载和立即加载?

懒加载: 在调用实例化方法之前获取实例对象(利用类加载方法)

立即加载: 在调用实例化方法之后获取实例对象

#### 线程安全的立即加载单例?(不使用synchronized)

```java
public class TestSigteon {
    private static TestSigteon testSigteon = new TestSigteon();

    private TestSigteon() {
    }

    public synchronized static TestSigteon getSigteonInstance() {
        return testSigteon;
    }
}
```

private static TestSignteon testSigteon = new TestSigteon();

是在调用实例化方法之后才去new TestSigteon()的


-> 等价改写

```java
public class TestSigteon {
    private static TestSigteon testSigteon;

    static {
        testSigteon = new TestSigteon();
    }

    private TestSigteon() {
    }

    public synchronized static TestSigteon getSigteonInstance() {
        return testSigteon;
    }
}
```

#### 静态内部类的特点

```java
public class Outter {

    public static void invokeInnerMethod() {
        System.out.println("调用内部类中的静态方法");
        Inner.InnerMethod();
    }

    public static void noInvokeInnerMethod() {
        System.out.println("没有调用内部类中的静态方法");
    }


    public static class Inner {

        static {
            System.out.println("这里是静态内部类");
        }

        public static void InnerMethod() {
            System.out.println("InnerMethod");
        }

    }
}
```

**Test**


```
public void test02(){
    Outter.invokeInnerMethod();
    Outter.noInvokeInnerMethod();
    Outter.invokeInnerMethod();
    Outter.invokeInnerMethod();
}
```

![](https://img.fengqigang.cn//img/20210624204427.png)

静态内部类的中 静态代码块只加载一次




#### 线程安全的懒加载单例?(不使用synchronized)

```java
public class TestSigteon {
    private static TestSigteon testSigteon;

    private TestSigteon() {
    }

    public static TestSigteon getInnerInstance() {
        return Inner.getSigteonInstance();
    }

    static class Inner {
        static {
            testSigteon = new TestSigteon();
        }

        static TestSigteon getSigteonInstance() {
            return testSigteon;
        }

    }
}
```


### 工厂模式

#### 简单工厂模式

1. 创建一个简单的工厂用来处理外面传进来的	`animal`

2. 实现一个 `animal` 对象, 其它的小动物继承 `animal` 对象


**factory**

```java
public class AnimalFactory {

    public Animal getAnimalS(String animal) {
        if ("Dog".equals(animal)) {
            return new Dog();
        } else if ("Fish".equals(animal)) {
            return new Fish();
        }

        return null;

    }
}
```

**animal**

```java
public class Animal {}
```

**Dog**

```java
public class Dog extends Animal{ }
```

**Fish**

```java
public class Fish extends Animal{}
```



#### 工厂方法

1. 创建一个工厂接口

2. 让其它money工厂实现这个接口

3. 实现money接口

4. 让其它的money实现这个接口



**MoneyFactory inteface**

```java
public interface MoneyFactory {
    public Money createMoney();
}
```

**money inteface**

```java
public interface Money {
}
```

**Dollar**

```java
public class Dollar implements Money{
}
```

**DollarFactory**

```java
public class DollarFactory implements MoneyFactory {

    @Override
    public Money createMoney() {
        return new Dollar();
    }
}
```


> DollarFactory 在写 createMoney 时, 写其实现子类即可

### 代理模式

#### 什么是静态代理和动态代理?

代理类需要自己写是静态代理

代理类不需要自己写是动态代理

#### 静态代理模式

#### 动态代理模式

![](https://img.fengqigang.cn//img/20210624215422.png)


- jdk 的动态代理

jdk 的动态代理的委托类对象与代理对象都会实现同一个接口

它们都是基于接口



```java
public interface UserService {
    public void sayHello();
    public void sayHello1(String name);
}
```

```java
public class UserServiceImpl implements UserService{
    @Override
    public void sayHello() {
        System.out.println("hello");
    }

    @Override
    public void sayHello1(String name) {
        System.out.println("bye bye " + name);

    }
}
```




```java
public class JDKDynamic {
    public static void main(String[] args) {
        UserServiceImpl userService = new UserServiceImpl();
        UserService userServiceImpl = (UserService) Proxy.newProxyInstance(UserServiceImpl.class.getClassLoader(), UserServiceImpl.class.getInterfaces(), new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

                Object invoke = method.invoke(userService, args);

                return invoke;
            }
        });

        userServiceImpl.sayHello1("孙");
    }
}
```

##### 保存生成的字节码文件

**ProxyGenerator**

![](https://img.fengqigang.cn//img/20210624222240.png)


![](https://img.fengqigang.cn//img/20210624222428.png)


![](https://img.fengqigang.cn//img/20210624222820.png)

设置working directory 放在当前module中

![](https://img.fengqigang.cn//img/20210624223057.png)


jdk 中的代理对象与委托类对象都是采取implement 同一个接口

![](https://img.fengqigang.cn//img/20210624223309.png)


- cGlib 的动态代理

1. 导入依赖

```xml
    <dependencies>
        <dependency>
            <groupId>cglib</groupId>
            <artifactId>cglib</artifactId>
            <version>3.2.12</version>
        </dependency>
    </dependencies>
```

2. CglibDynamic

```java
public class CglibDynamic {
    public static void main(String[] args) {


        UserServiceImpl userService = new UserServiceImpl();

        System.setProperty(DebuggingClassWriter.DEBUG_LOCATION_PROPERTY, "/Users/feng/Desktop/dynamicProxy");

        UserService userServiceImpl = (UserService) Enhancer.create(UserServiceImpl.class, new InvocationHandler() {
            @Override
            public Object invoke(Object o, Method method, Object[] objects) throws Throwable {
                Object invoke = method.invoke(userService, args);
                System.out.println("Bye Bye");
                return invoke;
            }
        });


        userServiceImpl.sayHello1("孙俪");
    }
}
```

cGlib 是采取继承的方式实现的


3. userService

```java
public interface UserService {
    public void sayHello();
    public void sayHello1(String name);
}
```

4. userServiceImpl

```java
public class UserServiceImpl implements UserService {
    @Override
    public void sayHello() {
        System.out.println("hello");
    }

    @Override
    public void sayHello1(String name) {
        System.out.println("bye bye " + name);

    }
}
```


![](https://img.fengqigang.cn//img/20210624225432.png)




