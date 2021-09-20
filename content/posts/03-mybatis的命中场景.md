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

## 一级缓存的特点

1. 默认打开

2. 底层是key-value形式


## 命中一级缓存测试


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
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
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

3. sqlSession 会话必须一样(会话级的缓存)

4. RowBounds 返回行范围必须相同

```java
@Test
public void test4(){
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
    Student student1 = mapper.selectById(2);
    Object student2 = sqlSession.selectOne("cn.fengqigang.mapper.StudentMapper.selectById", 2);

    System.out.println(student1 == student2);
}
```

**命中**

![20210919220906](https://img.fengqigang.cn//img/20210919220906.png)


```java
@Test
public void test5(){
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
    Student student1 = mapper.selectById(2);
    RowBounds rowBound = new RowBounds(0, 10);
    Object student2 = sqlSession.selectList("cn.fengqigang.mapper.StudentMapper.selectById", 2, rowBound);

    System.out.println(student1 == student2);
}
```

**未命中**

![20210919221358](https://img.fengqigang.cn//img/20210919221358.png)


```java
@Test
public void test5(){
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
    List<Student> student1 = mapper.selectById(2);
    RowBounds rowBound = RowBounds.DEFAULT;
    Object student2 = sqlSession.selectList("cn.fengqigang.mapper.StudentMapper.selectById", 2, rowBound);

    System.out.println(student1 == student2);
}
```

**命中**

![20210919222413](https://img.fengqigang.cn//img/20210919222413.png)



> 手动清空

```
@Test
public void test6(){
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
    List<Student> students = mapper.selectById(10);
    sqlSession.clearCache();
    List<Student> students1 = mapper.selectById(10);
    System.out.println(students == students1);
}
```

**未命中**

![20210919223726](https://img.fengqigang.cn//img/20210919223726.png)


> 执行updata 和 @Updata中写(select) 也会清空, 

```java
@Test
public void test7(){
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
    List<Student> students = mapper.selectById(2);
    mapper.setAge(2, 5);

    List<Student> students1 = mapper.selectById(2);
    System.out.println(students == students1);
}
```

![20210920200418](https://img.fengqigang.cn//img/20210920200418.png)


> 作用域缩小到statement

> 设置 localCacheScope 为 STATEMENT

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration  PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <settings>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <setting name="localCacheScope" value="STATEMENT"/>
    </settings>


    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC">
            </transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/test"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>

        </environment>
    </environments>
    <mappers>
        <!--<mapper resource="mapper/StudentMapper.xml" url="" class=""/>-->
        <package name="cn.fengqigang.mapper"/>
    </mappers>
</configuration>
```


```java
@Test
public void test8(){
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
    List<Student> students = mapper.selectById(2);

    List<Student> students2 = mapper.selectAll();

    List<Student> students1 = mapper.selectById(2);
    System.out.println(students == students1);
}
```

![20210920202424](https://img.fengqigang.cn//img/20210920202424.png)

> 执行 session.comit 或 session.rollback 也会清空缓存, 会调用 clearLocalcache

```java
@Test
public void test9(){
    StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
    List<Student> students = mapper.selectById(2);

    sqlSession.commit();
    sqlSession.rollback();

    List<Student> students1 = mapper.selectById(2);
    System.out.println(students == students1);
}
```


## 总结

![20210920203012](https://img.fengqigang.cn//img/20210920203012.png)


