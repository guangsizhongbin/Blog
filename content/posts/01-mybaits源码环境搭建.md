---
title: "01 Mybaits源码环境搭建"
date: 2021-09-12T23:11:24+08:00
lastmod: 2021-09-12
author: "xiaonan"
math:
 enable: true

tags: 
- mybatis
categories: []
- mybatis
---

## 克隆`mybatis`仓库


mybatis: https://github.com/mybatis/mybatis-3

parent: https://github.com/mybatis/parent

## 编译

1. 先编译parent

2. 后编译mybatis

## 创建一个maven项目

1. 删掉其src, 创建一个springboot module

![20210912225117](https://img.fengqigang.cn//img/20210912225117.png)

2. 测试springboot项目是否可以启动

## 添加之前的mybatis项目

![20210912225622](https://img.fengqigang.cn//img/20210912225622.png)

## 添加mybatis为新项目的依赖

![20210912225706](https://img.fengqigang.cn//img/20210912225706.png)

## 测试mybatis是否搭建成功

![20210912230059](https://img.fengqigang.cn//img/20210912230059.png)

![20210912230227](https://img.fengqigang.cn//img/20210912230227.png)

1. bean

```java
import lombok.Data;

@Data
public class Student {
    private int id;
    private String name;
    private int age;
}
```

2. StudentMapper

```java
import cn.fengqigang.bean.Student;

public interface StudentMapper {
   Student selectById(Integer id);
}
``

3. MyTest

```java
import cn.fengqigang.bean.Student;
import cn.fengqigang.mapper.StudentMapper;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.Reader;

public class MyTest {
    private static SqlSessionFactory sqlSessionFactory;

    public static void main(String[] args) throws IOException {
       String resource = "mybatis-config.xml";

        final Reader reader = Resources.getResourceAsReader(resource);
        sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);
        reader.close();

        SqlSession sqlSession = sqlSessionFactory.openSession();

        StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);

        Student student = mapper.selectById(2);
        System.out.println(student);
    }
}
```
4. StudentMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="cn.fengqigang.mapper.StudentMapper">

    <select id="selectById" resultType="cn.fengqigang.bean.Student">
      select * from student where id = #{id}
    </select>
</mapper>
```

5. mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration  PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
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

## 添加新的依赖

```xml
	<dependency>
			<groupId>org.javassist</groupId>
			<artifactId>javassist</artifactId>
			<version>3.24.1-GA</version>
		</dependency>

		<dependency>
			<groupId>ognl</groupId>
			<artifactId>ognl</artifactId>
			<version>3.1.12</version>
		</dependency>
```

## 运行

![20210912230700](https://img.fengqigang.cn//img/20210912230700.png)









`

