---
title: "02 Spring测试源码学习环境是否搭建成功"
date: 2021-08-24T23:57:01+08:00
lastmod: 2021-08-24
author: "xiaonan"
math:
 enable: true

tags: 
- spring
- 源码学习

categories:
- spring源码学习

---

## 新建`module`

1. 新建 `moudle`

![20210824224818](https://img.fengqigang.cn//img/20210824224818.png)

2. 选择 `gradle` 项目(spring-study)

![20210824225058](https://img.fengqigang.cn//img/20210824225058.png)

## 查看项目是否导入成功

在整个项目的 `settings.gradle` 是否引入 `spring-study` 项目

![20210824230259](https://img.fengqigang.cn//img/20210824230259.png)

## 设置项目依赖

在新建的 `moudle` 下打开 `build.gradle` 引入下面的依赖 `spring-beans`, `spring-context`, `spring-core`, `spring-expression`, `spring-instrument`

![20210824230034](https://img.fengqigang.cn//img/20210824230034.png)

## 新建测试 `bean`

![20210824225150](https://img.fengqigang.cn//img/20210824225150.png)

1. `cn.fengqigang.bean.Person`

```java
package cn.fengqigang.bean;

public class Person {
	private String name;

	private int age;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}

	public Person() {
	}

	@Override
	public String toString() {
		return "Person{" +
				"name='" + name + '\'' +
				", age=" + age +
				'}';
	}
}
```

2. `person.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean class="cn.fengqigang.bean.Person" id="person">
        <property name="name" value="fengqigang"/>
        <property name="age" value="22"/>
    </bean>
</beans>
```

3. `DemoMain.java`

```java
package cn.fengqigang.start;

import cn.fengqigang.bean.Person;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class DemoMain {
	public static void main(String[] args) {
		ClassPathXmlApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("person.xml");
		Person bean = classPathXmlApplicationContext.getBean(Person.class);

		System.out.println(bean);
	}
}
```

## 测试

![20210824230338](https://img.fengqigang.cn//img/20210824230338.png)


