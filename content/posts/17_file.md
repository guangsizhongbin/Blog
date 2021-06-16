---
title: "17_file"
date: 2021-04-18T23:19:15+08:00
lastmod: 2021-04-18
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

###  什么是 **File** 类?

**File** 类位于 **java.io** 包下， 是 **java** 进行 **IO** 操作的核心类， **File** 也是 **I/O** 的前置知识点

**File** 是文件和目录(文件夹)路径名的抽象表达形式


**File类只是用文件/夹的路径来抽象的表示文件，那么这个路径下是否真的存在这个文件，它并不关心**


**File类在创建对象时，不关心文件是否存在，也不会抛出任何异常**

### 如何获取当前 **idea** 相对路径?

**System.getProperty("user.dir")**

```java
public class demo {
    public static void main(String[] args) {
        System.out.println(System.getProperty("user.dir"));
    }
}
```

![20210415192721](https://img.fengqigang.cn//img/20210415192721.png)

### **Java** 如何转义路径?

可以用 **//**, **\\**

### 如何判断当前目录下 **a** 是否存在?

**public boolean exists()**

**绝对路径**

```java
public class demo {
    public static void main(String[] args) {
        File f = new File("/home/feng/IdeaProjects/day13/a");
        System.out.println(f.exists());
    }
}
```

**相对路径**

```java
public class demo {
    public static void main(String[] args) {
        File f = new File("a");
        System.out.println(f.exists());
    }
}
```

### 如何判断 **/home/feng/IdeaProjects/day13** 下的 **a** 是否存在, 分开写?

```java
public class demo {
    public static void main(String[] args) {
        File f = new File("/home/feng/IdeaProjects/day13", "a");
        System.out.println(f.exists());
    }
}
```

**转义后**


```java
public class demo {
    public static void main(String[] args) {
        File f = new File("//home//feng//IdeaProjects//day13", "a");
        System.out.println(f.exists());
    }
}
```

### 如何将子路径用 **tempFile**, 查找 **/home/feng/IdeaProjects/day13** 下有没有 **a** 文件

```java
public class demo {
    public static void main(String[] args) {
        File tempFile = new File("//home//feng//IdeaProjects//day13");
        File f4 = new File(tempFile, "a");
        System.out.println(f4.exists());
    }
}
```

### 如何查看 **系统有关** 的多个路径名的 **分隔符** 和 **单个路径层级的分隔符** ?

**File.pathSeparator**

**File.separator**

```java
public class demo {
    public static void main(String[] args) {
        System.out.println(File.pathSeparator);
        System.out.println(File.separator);
    }
}
```

![20210415194714](https://img.fengqigang.cn//img/20210415194714.png)

### 如何创建一个文件 **1.txt**?

**createNewFIle**

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("1.txt");
        System.out.println(f1.createNewFile());
    }
}
```

### 如何创建一个目录 **abc**?

**mkdir**

不能创建多级目录

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("abc");
        System.out.println(f1.mkdir());
    }
}
```

### 如何创建 **a/b/c** 这种三级目录?

**mkdirs**

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("a//b//c");
        System.out.println(f1.mkdirs());
    }
}
```

### 如何删除 **1.txt**

**delete**

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("1.txt");
        System.out.println(f1.delete());
    }
}
```

### 如何删除一个不是空的目录?

**递归删除非空目录**

1. 获取这个目录下的所有文件和文件夹的对象

2. 做判断:

如果是文件, 直接删除

如果是目录，看它是不是空目录，如果是空目录，直接删除

如果不是空目录，递归去删除

### 如何将创建一个1文件并将其改名为2?

**renameTo**

public boolean renameTo (File dest)

Renames the file denoted by this abstract pathname.

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("1");
        f1.createNewFile();
        File f2 = new File("2");
        System.out.println(f1.renameTo(f2));
    }
}
```

### 如何判断 **1** 是否表示一个文件?

**isFile()**

public boolean isFile()

Tests whether the file denoted by this abstract pathname is a normal file. 

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("1");
        System.out.println(f1.isFile());
    }
}
```

### 如何判断 **1** 是否表示一个目录?

**isDirectory**

public boolean isDirectory()

Tests whether the file denoted by the this abstract pathname is a directory

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("2");
        System.out.println(f1.isDirectory());
    }
}
```

### 如何判断 **2** 是否存在?

**exists**

public boolean exists()

Tests whether the file or directory denoted by this abstract pathname exists.

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("2");
        System.out.println(f1.exists());
    }
}
```

### 如何获取 **2** 文件或者目录的文件名?

**getName**

public String getName()

Returns the name of of the file or directory denoted by this abstract pathname.

```java
public class demo {
    public static void main(String[] args) throws IOException {
        File f1 = new File("2");
        System.out.println(f1.getName());
    }
}
```

### 如何遍历一个文件夹?

```java
public class Demo {
    public static void main(String[] args) {
        File f = new File(".");
        String[] list = f.list();

        System.out.println("增强for循环");
        for (String s : list) {
            System.out.println(s);
        }

        System.out.println("-------------------");
        System.out.println("toString");
        System.out.println(Arrays.toString(list));
    }
}
```

### 如何遍历一个文件夹 (listFiles 数组)?

```java
public class Demo {
    public static void main(String[] args) {
        File f = new File(".");
        File[] files = f.listFiles();

        for (int i = 0; i < files.length; i++) {
            System.out.println(files[i].getPath());
        }
    }
}
```

![20210415211945](https://img.fengqigang.cn//img/20210415211945.png)

### 如何查看学习资料(对象必须是一个 **文件** , 文件的后缀是 **.mp4**)? 用匿名内部类

```java
public class Demo {
    public static void main(String[] args) {
        File f = new File(".");
        File[] files = f.listFiles(new FileFilter() {
            @Override
            public boolean accept(File pathname) {
                String fileName = pathname.getName();
                return pathname.isFile() && fileName.endsWith(".mp4");
            }
        });
        System.out.println(Arrays.toString(files));
    }
}

class MyFileFilter implements FileFilter {
    @Override
    public boolean accept(File pathname) {
        return true;
    }
}
```

![20210415213358](https://img.fengqigang.cn//img/20210415213358.png)

### 如何查看学习资料(对象必须是一个 **文件** , 文件的后缀是 **.mp4**)? 用lambda表达式?

```java
public class Demo {
    public static void main(String[] args) {
        File f = new File(".");
        File[] files = f.listFiles((file) -> {
            String fileName = file.getName();
            boolean beyond = fileName.startsWith("Beyond");
            boolean filel = file.isFile();
            return filel && beyond;
        });
        System.out.println(Arrays.toString(files));
    }
}

class MyFileFilter implements FileFilter {
    @Override
    public boolean accept(File pathname) {
        return true;
    }
}
```

![20210415214242](https://img.fengqigang.cn//img/20210415214242.png)

### 如何使用 **lambda** 表达式实现只看 文件夹中的文件?

```java
public class Demo {
    public static void main(String[] args) {
        File f = new File(".");
        File[] file = f.listFiles(File::isFile);
        System.out.println(Arrays.toString(file));
    }
}
```

![20210415214549](https://img.fengqigang.cn//img/20210415214549.png)

### **@Deprecated** 是什么意思?

这些方法往往都已经被新的方法替代了，但是这些方法没有被删除


### 如何实现递归删除目录?

```java
public class Work3 {
    public static void main(String[] args) {
        File file = new File("E:\\1");
        System.out.println("是否已经删完?" + deleteDirectory(file));
    }

    public static boolean deleteDirectory(File target) {
        File[] files = target.listFiles();

        if (files == null || files.length == 0) {
				// files == null 为文件， files.length 为空目录
            return target.delete();
        }

        for (File file : files) {
            if (file.isDirectory()) {
						//如果是文件夹，删除里面的文件
                deleteDirectory(file);
            } else {
                file.delete();
            }
        }

        return target.delete();
    }
}
```

