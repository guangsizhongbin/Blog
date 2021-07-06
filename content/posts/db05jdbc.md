---
title: "Db05jdbc"
date: 2021-07-06T16:56:02+08:00
lastmod: 2021-07-06
author: "xiaonan"
math:
 enable: true

tags: [jdbc]
categories: [王道]
---

### 数据库的访问过程是什么样的?

1. 客户端与 `Mysql` 服务器之间建立连接

- 加载驱动 

DriverManager.registerDriver(new Driver())

- 获取连接对象

Connection connection = DriverManager.getConnection(url, name, password);

2. 客户端与 `Mysql` 服务器发送数据库请求

Statement statement = connection.createStatement();

3. `Mysql` 服务器处理客户端的相应，并返回结果给客户端

statement.executeUpdate()
statement.executeQuery()

4. 客户端接受 `Mysql`服务器的相应，并按照自己的业务逻辑做相应处理

5. 释放相关资源

statement

connection

resultSet

### 如何设置 `jdbc` 使用 `mydatabase` 数据库？

开始使用参数用? 再接参数时使用&

```xml
url=jdbc:mysql://localhost:3306/mydatabase;
```

### 如何设置 `jdbc` 使用 `mydatabase` 数据库, 并不使用SSL?

开始使用参数用? 再接参数时使用&

```xml
url=jdbc:mysql://localhost:3306/mydatabase?useSSL=false;
```

### 如何设置 `jdbc` 使用 `mydatabase` 数据库, 并不使用SSL, 设置编码格式为utf8?

开始使用参数用? 再接参数时使用&

```xml
url=jdbc:mysql://localhost:3306/mydatabase?useSSL=false&characterEncoding=utf8;
```

### 如何设置 `jdbc` 使用 `mydatabase` 数据库, 并不使用SSL, 设置编码格式为utf8, 并使用 `serverTimezone=Asia/Shanghai`?

开始使用参数用? 再接参数时使用&

```xml
url=jdbc:mysql://localhost:3306/mydatabase?useSSL=false&characterEncoding=utf8&serverTimezone=Asia/Shanghai;
```

### 如何设置 `jdbc` 使用 `mydatabase` 数据库, 并不使用SSL, 设置编码格式为utf8, 并使用 `serverTimezone=Asia/Shanghai`, 并使用批出理?

开始使用参数用? 再接参数时使用&

```xml
url=jdbc:mysql://localhost:3306/mydatabase?useSSL=false&characterEncoding=utf8&serverTimezone=Asia/Shanghai&rewriteBatchedStatements=true;
```

### 若要设置 `driverClassName`， 应该如何设置?

```xml
driverClassName=com.mysql.jdbc.Driver
```

### 怎么会产生数据库注入的问题?

```sql
select * from user where '1=1' and username = '123' and password = '123';
```

会导致 `1=1` 始终为真, 后面无论怎么输入都是正确的

### 怎样防止数据库注入问题?

采用预编译的方法 

prepareStatement

```java
PreparedStatement prepareStatement = connection.prepareStatement("select * from user where username = ? and password = ?")

prepareStatement.setString(1, 'feng');
prepareStatement.setString(2, '123');

ResultSet resultSet = prepareStatement.executeQuery();
```

`?` 代表占位符

### `prepareStatement` 与 `statement` 有什么区别?

`prepareStatement` 会与服务器通信二次

`statement` 只会与服务器通信一次

### 什么是 `JDBC` 批处理?

![20210706161939](https://img.fengqigang.cn//img/20210706161939.png)

### 如何使用 `JDBC` 批处理(非预处理)?

```java
Statement statement = connection.createStatement();

statement.addBatch("insert into user values (null, 'lisi', 'lisi')")
statement.addBatch("insert into user values (null, 'libai', 'libai')")

int[] ints = statement.executeBatch();

for (int anInt : ints) {
	System.out.println("affectedRow:" + anInt);
}
```


### 如何使用 `JDBC` 批处理(预处理)?

```java
PreparedStatement prepareStatement = connection.prepareStatement("insert into user values (null, ?, ?)");

prepareStatement.setString(1, "sun");
prepareStatement.setString(2, "sun");
prepareStatement.addBatch();

prepareStatement.setString(1, "se");
prepareStatement.setString(2, "se");
prepareStatement.addBatch();

int[] ints = prepareStatement.executeBatch();

for (int anInt : ints){
	System.out.println("affectedRows:" + anInt);
}
```
