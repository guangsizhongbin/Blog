---
title: "Spring02"
date: 2021-06-25T23:23:09+08:00
lastmod: 2021-06-25
author: "xiaonan"
math:
 enable: true

tags: [spring]
categories: [王道]
---
02_Spring

### builder 设计模式

> 注意

![20210625201410](https://img.fengqigang.cn//img/20210625201410.png)

如果setIq 和 sethair 方法中的 head, 如果没有初始化的话会出现空指针异常


>> 处理方法:

![20210625201554](https://img.fengqigang.cn//img/20210625201554.png)

**HumanBuilder**

```java
public class HumanBuilder {
    Human human = new Human();

    public Head setIq(Integer iq) {
        Head head = human.getHead();
        head.setIq(iq);
        return head;
    }

    public Head setHair(String hair) {
        Head head = human.getHead();
        head.setHair(hair);
        return head;
    }
}
```

**Human**

```java
@Data
public class Human {
    Head head = new Head();
    Body body = new Body();
    Leg leg = new Leg();
}
```

**head**

```java
@Data
public class Head {
    Integer iq;
    String hair;
}
```

**Leg**

```java
@Data
public class Leg {
}
```

### builder 设计模式进一步思考?

实现不停的 setHead 和 setHair

可以在Humanbuilder中return builer


```java
@Data
public class HumanBuilder {
    Human human = new Human();

    public HumanBuilder setIq(Integer iq) {
        Head head = human.getHead();
        head.setIq(iq);
        return this;
    }

    public HumanBuilder setHair(String hair) {
        Head head = human.getHead();
        head.setHair(hair);
        return this;
    }
}
```


### Spring 入门案例一

1. 引入依赖

2. 在 `resources` 中写下application.xml的配置文件

3. 单元测试

- 获取实例

- getBean


#### 引入依赖

(5 + 1) 5.25 RELEASE

context

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.5.RELEASE</version>
    </dependency>
</dependencies>
```

#### 在resours 中写下application.xml的配置文件

![20210625210326](https://img.fengqigang.cn//img/20210625210326.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!-- bean definitions here -->
    <bean id="userService" class="cn.fengqigang.SpringIoc.UserServiceIml"/>
    <bean id="userService1" class="cn.fengqigang.SpringIoc.UserServiceIml"/>
</beans>
```

#### 单元测试

- **UserService**

```java
public interface UserService {
    void sayHello();

    void sayHello1(String name);
}
```

- **UserServiceIml**

```java
public class UserServiceIml implements UserService {

    @Override
    public void sayHello() {
        System.out.println("hello somebody");
    }

    @Override
    public void sayHello1(String name) {
        System.out.println("hello" + name);
    }
}
```

- junit


![20210625211237](https://img.fengqigang.cn//img/20210625211237.png)

> applicationContext.getBean 的三种方式

1. id(String)

2. class

**当该类型的组件只有一个的时候,才可以通过类型取出**

此时 `UserService.class` 有两个, 会出现报错

![20210625211649](https://img.fengqigang.cn//img/20210625211649.png)

3. String + class


> 单例与不同的组件是什么关系?

```java
    public void testSpring03(){
        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("application.xml");

        UserService userService1 = applicationContext.getBean("userService", UserService.class);
        UserService userService2 = applicationContext.getBean("userService", UserService.class);
        UserService userService3 = applicationContext.getBean("userService", UserService.class);

        UserService userServicea = applicationContext.getBean("userService1", UserService.class);
        UserService userServiceb = applicationContext.getBean("userService1", UserService.class);
        UserService userServicec = applicationContext.getBean("userService1", UserService.class);


    }
```

![20210625212717](https://img.fengqigang.cn//img/20210625212717.png)

一个组件实现一个单例



### 入门案例二(注册多个组件并且有关联关系)

```java
    @Test
    public void test02() {
        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("application.xml");
        UserService userService = applicationContext.getBean(UserService.class);
        userService.sayHello();
    }
```


![](https://img.fengqigang.cn//img/20210625221254.png)


不设置时

![20210625221417](https://img.fengqigang.cn//img/20210625221417.png)


#### Bean实例化

##### 构造方法

- 无参构造

- 有参构造

![20210625222954](https://img.fengqigang.cn//img/20210625222954.png)



#### 工厂

- 静态工厂

factroy-method 为静态工厂中的方法

![](https://img.fengqigang.cn//img/20210625224111.png)

- 实例工厂

![20210625224341](https://img.fengqigang.cn//img/20210625224341.png)

factory-bean 为实例工厂的id

factory-method 为工厂中的方法


- FactroyBean


继承 FactroyBean

![20210625224807](https://img.fengqigang.cn//img/20210625224807.png)


### Bean的作用域

**singleton**

**prototype**

![20210625225005](https://img.fengqigang.cn//img/20210625225005.png)

### 生命周期


![20210625230225](https://img.fengqigang.cn//img/20210625230225.png)

**BeanPostProcessor**

除了BeanPostProcessor组件本身,其他所有的组件都会执行到对应的方法

**implements BeanPostProcessor**

- postProcessBeforInitialization

- postProcessAfterInitialization

![20210625230831](https://img.fengqigang.cn//img/20210625230831.png)



自定义的方法

Init-method="xxxx"

![](https://img.fengqigang.cn//img/20210625225947.png)








