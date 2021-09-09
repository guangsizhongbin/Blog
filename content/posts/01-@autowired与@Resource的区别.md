---
title: "01 @Autowired与@Resource的区别"
date: 2021-09-09T22:30:23+08:00
lastmod: 2021-09-09
author: "xiaonan"
math:
 enable: true

tags: 
- spring
categories:
- spring
---

## 区别
> 1. 来源不同

@Resource是java自带的

@AutoWired是spring带来的

![20210901210537](https://img.fengqigang.cn//img/20210901210537.png)


> 2. 注入的方式不同

`@Autowired` 只按照 `byType` 注入

出现多个实现`bean`时可以用`@Primary` 来修饰也可以用`@Qualifier`来标注需要注入的类

`@Resource` 默认按 `byName` 注入

出现多个实现`bean`时可以用`name=xxx`来指定

## 实战


![20210901211144](https://img.fengqigang.cn//img/20210901211144.png)

- HumanController

```java
@RestController
@RequestMapping("/an")
public class HumanController {

    @Autowired
    private Human human;

    @RequestMapping("/run")
    public String runMarathon(){
        return human.runMarathon();
    }
}
```

- Human

```java
public interface Human {
    String runMarathon();
}
```

- Man 

```java
@Service
public class Man implements Human {

    @Override
    public String runMarathon() {
        return "A man run marathon";
    }
}
```

- Woman


```java
@Service
public class Woman implements Human {
    @Override
    public String runMarathon() {
        return "An woman run marathon";
    }
}
```

> 1. 加入@Primary, 帮助@autowired找到对应的实现类

![20210901211924](https://img.fengqigang.cn//img/20210901211924.png)

> 2. 使用@autowired时，也可以加入@Qualifier("xxx")来指定

![20210901212513](https://img.fengqigang.cn//img/20210901212513.png)


> 3. 使用@Resource时, 指定name, name后的名字要小写

![20210901212043](https://img.fengqigang.cn//img/20210901212043.png)

> 4. 使用@Resource时，再加入@Qualifier("xxx")来指定

![20210901212329](https://img.fengqigang.cn//img/20210901212329.png)




