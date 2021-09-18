---
title: "02 Mybatis执行器"
date: 2021-09-13T22:39:42+08:00
lastmod: 2021-09-14
author: "xiaonan"
math:
 enable: true

tags:
- mybatis
categories:
- mybatis
---

## mybatis的四大模块

1. 动态代理 MapperProxy

2. SQL 会话 SqlSession

3. 执行器 Executor

4. JDBC StatementHandler

![20210913223133](https://img.fengqigang.cn//img/20210913223133.png)

## Mybatis的执行过程

门面模式:

提供一个`统一的门面接口API`, 使得系统更容易使用

![20210913223517](https://img.fengqigang.cn//img/20210913223517.png)


### 执行器

#### 1. 简单执行器(SimpleExecutor)

无论SQL是否一样，每次都会进行预编译

```java
package cn.fengqigang.test;

import cn.fengqigang.bean.JDBC;
import org.apache.ibatis.executor.SimpleExecutor;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.mapping.MappedStatement;
import org.apache.ibatis.session.Configuration;
import org.apache.ibatis.session.RowBounds;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.apache.ibatis.transaction.jdbc.JdbcTransaction;
import org.junit.Before;
import org.junit.Test;

import jav.io.IOException;
import java.io.Reader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.List;

public class ExecutorTest {
    private Configuration configuration;
    private Connection connection;
    private JdbcTransaction jdbcTransaction;

    @Before
    public void init() throws SQLException, IOException {
        String resource = "mybatis-config.xml";
        final Reader reader = Resources.getResourceAsReader(resource);
        SqlSessionFactory build = new SqlSessionFactoryBuilder().build(reader);
        configuration = build.getConfiguration();
        connection = DriverManager.getConnection(JDBC.URL, JDBC.USERNAME, JDBC.PASSWORD);
        jdbcTransaction = new JdbcTransaction(connection);
    }

    @Test
    public void simpleTest() throws SQLException {
        SimpleExecutor executor = new SimpleExecutor(configuration, jdbcTransaction);
        MappedStatement ms = configuration.getMappedStatement("cn.fengqigang.mapper.StudentMapper.selectById");
        List<Object> list1 = executor.doQuery(ms, 2, RowBounds.DEFAULT,
                SimpleExecutor.NO_RESULT_HANDLER, ms.getBoundSql(2));
        List<Object> list2 = executor.doQuery(ms, 2, RowBounds.DEFAULT,
                SimpleExecutor.NO_RESULT_HANDLER, ms.getBoundSql(2));
        System.out.println(list1.get(0));
        System.out.println(list2.get(0));
    }
}
```

![20210915231029](https://img.fengqigang.cn//img/20210915231029.png)

#### 2. 可重用执行器(ReuseExecutor)

相同的SQL只进行一次预处理

```java
@Test
public void ReuseTest() throws SQLException {
    ReuseExecutor executor = new ReuseExecutor(configuration, jdbcTransaction);
    MappedStatement ms = configuration.getMappedStatement("cn.fengqigang.mapper.StudentMapper.selectById");
    List<Object> list1 = executor.doQuery(ms, 2, RowBounds.DEFAULT,
            SimpleExecutor.NO_RESULT_HANDLER, ms.getBoundSql(2));
    List<Object> list2 = executor.doQuery(ms, 2, RowBounds.DEFAULT,
            SimpleExecutor.NO_RESULT_HANDLER, ms.getBoundSql(2));
    System.out.println(list1.get(0));
    System.out.println(list2.get(0));
}
```

![20210916191458](https://img.fengqigang.cn//img/20210916191458.png)

#### 3. 批处理执行器(Batch Executor)

批处理提交修改

必须执行flushStatements才会生效

> **只针对修改操作, 而对增删操作无效**

```java
// 只针对修改操作
// 批处理必须手动刷新
@Test
public void BatchTest() throws SQLException {
    BatchExecutor executor = new BatchExecutor(configuration, jdbcTransaction);
    MappedStatement setAge = configuration.getMappedStatement("cn.fengqigang.mapper.StudentMapper.setAge");
    Map param = new HashMap<>();
    param.put("arg0", 2);
    param.put("arg1", 1);
    executor.doUpdate(setAge, param);
    executor.doUpdate(setAge, param);
    executor.doFlushStatements(false);
}
```

![20210916192142](https://img.fengqigang.cn//img/20210916192142.png)

> 批处理操作必须手动刷新

![20210916193934](https://img.fengqigang.cn//img/20210916193934.png)




![20210914230935](https://img.fengqigang.cn//img/20210914230935.png)

#### 4. Base Executor(负责一级缓存和获取连接)

```java
@Test
public void BaseExecutorTest() throws SQLException {
    Executor executor = new SimpleExecutor(configuration, jdbcTransaction);
    MappedStatement ms = configuration.getMappedStatement("cn.fengqigang.mapper.StudentMapper.selectById");
    executor.query(ms, 10, RowBounds.DEFAULT, Executor.NO_RESULT_HANDLER);
    executor.query(ms, 10, RowBounds.DEFAULT, Executor.NO_RESULT_HANDLER);
}
```

#### 5. Caching Executor(获取二级缓存)


```java
@Test
public void cacheExecutorTest() throws SQLException {
    SimpleExecutor executor = new SimpleExecutor(configuration, jdbcTransaction);

    CachingExecutor cachingExecutor = new CachingExecutor(executor); // 二级缓存相关逻辑 执行数据操作逻辑
    MappedStatement ms = configuration.getMappedStatement("cn.fengqigang.mapper.StudentMapper.selectById");

    cachingExecutor.query(ms, 3, RowBounds.DEFAULT, Executor.NO_RESULT_HANDLER);
    cachingExecutor.query(ms, 3, RowBounds.DEFAULT, Executor.NO_RESULT_HANDLER);
}
```



装饰者模式:

在不改变原有类结构和继承的情况下，通过包装原对象去扩展一个新功能.

![20210917231606](https://img.fengqigang.cn//img/20210917231606.png)

> 一级缓存与二级缓存的区别?

1. 一级缓存, 在查询之后，缓存中的数据立马就有了

2. 二级缓存需要提交之后，缓存才会存在

3. 二级缓存存在跨线程的调用，而一级缓存不会


#### 6. SessionExector

```java
@Test
public void sessionTest(){
    SqlSession sqlSession = factory.openSession(true);
    // 降低调用的复杂性
    List<Object> list = sqlSession.selectList("cn.fengqigang.mapper.StudentMapper.selectById", 3);
    System.out.println(list.get(0));
}
```

![20210918213105](https://img.fengqigang.cn//img/20210918213105.png)
