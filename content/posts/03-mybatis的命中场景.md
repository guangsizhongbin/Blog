---
title: "03 Mybatis的命中场景"
date: 2021-09-18T23:17:19+08:00
lastmod: 2021-09-18
author: "xiaonan"
math:
 enable: true

tags:
- mybatis
categories:
- mybatis
---

## 命中一级缓存测试

> 一级缓存命中的条件

1. SQL 和参数必须相同

2. 相同的 statement id



```java
public class FirstCacheTest {
    private SqlSessionFactory factory;
    private SqlSession sqlSession;

    @Before
    public void init() {
        // 获取构建器
        SqlSessionFactoryBuilder factoryBuilder = new SqlSessionFactoryBuilder();
        // 解析XML 并构建会话工厂
        factory = factoryBuilder.build(ExecutorTest.class.getResourceAsStream("/mybatis-config.xml"));
        sqlSession = factory.openSession();
    }

    @Test
    public void test1() {
        StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
        Student student1 = mapper.selectById(2);
        Student student2 = mapper.selectById(2);
        System.out.println(student1 == student2);
    }
}
```

![20210918214410](https://img.fengqigang.cn//img/20210918214410.png)

**命中**


```java
@Test
public void test2() {
    StudentMapper mapper = sqlSession.getMapper(StudentMpper.class);
    Student student = mapper.selectById(2);
    Student student1 = mapper.selectById1(2);
    System.out.println(student == student1);
}
```

**未命中, statement ID 不相同**

![20210918215205](https://img.fengqigang.cn//img/20210918215205.png)

### 什么时候会导致不同的Statement ID?

1. sql 和参数不相同

2. 不相同的statementID

3. sqlSession 会话必须一样

```java

```


a

