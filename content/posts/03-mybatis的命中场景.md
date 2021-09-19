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







