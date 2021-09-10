---
title: "02 SpringBoot加载配置文件"
date: 2021-09-10T23:49:36+08:00
lastmod: 2021-09-10
author: "xiaonan"
math:
 enable: true

tags:
- spring
categories:
- spring
---

## springboot的自动化配置

默认情况下 `springboot` 会自动读取 `application.properties` 和 `application.yaml` 

## 使用 `application.yaml` 中的配置

1. `@Value()`

- `application.yaml`

```yaml
config: hello, fengqigang
```

使用

- `HelloControl`

```java
@RestController
public class HelloControl {

    @Value("${config}")
    private String config;

    @RequestMapping("/index")
    public void say() {
        System.out.println(config);
    }
}
```

2. 配置成实体类

- `BeanConfig`

```java
@Data
@Component
@ConfigurationProperties(prefix = "config2")
public class BeanConfig {
    public String name;
    public String value;
}
```

- `BeanController`

```java
@RestController
public class BeanController {

    @Autowired
    public BeanConfig beanConfig;

    @RequestMapping("/say")
    public void say(){
        System.out.println(beanConfig);
    }
}
```

> 使用@Autowired注入

## 使用自定义的配置文件如 `testaa.properties`

![20210901132644](https://img.fengqigang.cn//img/20210901132644.png)

- `testaa.properties`

```
aaa.a1=aa1123
aaa.a2=aa2123
aaa.a3=aa3123
aaa.a4=aa4123
```

- `ConfigPojo`

```java
public class ConfigPojo {
    public String a1 = null;
    public String a2 = null;
    public String a3 = null;
    public String a4 = null;
}
```

- `ConfigTest`

```java
@Configuration
@PropertySource("classpath:testaa.properties")
public class ConfigTest {

    @Value("${aaa.a1}")
    String a1;

    @Value("${aaa.a2}")
    String a2;

    @Value("${aaa.a3}")
    String a3;

    @Value("${aaa.a4}")
    String a4;

    @Bean
    public ConfigPojo getAaa() {
        ConfigPojo cp = new ConfigPojo();
        cp.a1 = a1;
        cp.a2 = a2;
        cp.a3 = a3;
        cp.a4 = a4;

        return cp;
    }
}
```

> 使用 `@PropertySource("classpath:testaa.properties")`, 设定配置路径










