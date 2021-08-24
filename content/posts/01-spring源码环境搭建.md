---
title: "01 Spring源码环境搭建"
date: 2021-08-24T23:54:53+08:00
lastmod: 2021-08-24
author: "xiaonan"
math:
 enable: true

tags: 
- 源码学习
- spring

categories:
- spring源码学习

---

## 克隆spring `5.1.x` 源代码

```bash
git clone -b 5.1.x https://github.com/spring-projects/spring-framework.git
```

## 查看导入idea的需要注意的事项，并执行

1. Precompile `spring-oxm` with `./gradlew :spring-oxm:compileTestJava`


`import-into-idea.md`

在 `spring-framework` 文件夹下运行以下命令

```bash
./gradlew :spring-oxm:complieTestJavals
```

等待大约7分钟

![20210824214735](https://img.fengqigang.cn//img/20210824214735.png)

2. Import into IntelliJ (File -> New -> Project from Existing Sources -> Navigate to directory -> Select build.gradle)


3. When prompted exclude the `spring-aspects` module (or after the import via File-> Project Structure -> Modules)

![20210824221451](https://img.fengqigang.cn//img/20210824221451.png)

4. code away








