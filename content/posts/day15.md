---
title: "Day15"
date: 2021-04-15T21:58:11+08:00
lastmod: 2021-04-15
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 如何 **catch**， 判断是否实现空接口?  ![20210415171814](https://img.fengqigang.cn//img/20210415171814.png)

```java
public class demo {
    public static void main(String[] args) {
        A a = new A();
        try {
            checkCloneable(a);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
            System.out.println("请实现空接口!");
        }
        System.out.println("111");
    }


    private static void checkCloneable(A a) throws CloneNotSupportedException {
        if (a instanceof Cloneable) {
            System.out.println("实现了Cloneable接口，允许进行克隆操作, 程序正常执行");
        } else {
            throw new CloneNotSupportedException("没有实现Cloneable接口");
        }
    }
}

interface Cloneable {
}

class A {
}
```

![20210415172058](https://img.fengqigang.cn//img/20210415172058.png)

### 在设置年龄时大于150抛出异常"你活不了这么大", 小于0抛出异常"你还没出生吗? ![20210415173941](https://img.fengqigang.cn//img/20210415173941.png)

```java
public class demo {
    public static void main(String[] args) {
        Student s = new Student();
        s.setAge(151);

    }
}

class Student {
    public int age;

    public Student() {
    }

    public void setAge(int age) {
        if (age > 150) {
            throw new IllegalArgumentException("你活不能这么大");
        } else if (age < 0) {
            throw new IllegalArgumentException("你还没出生吗？");
        } else {
            this.age = age;
        }
    }
}
```

![20210415174031](https://img.fengqigang.cn//img/20210415174031.png)

### 编译期异常和运行期异常有什么区别?

**编译期异常**

必须要显式处理，否则编译不通过

**运行期异常**

可以不处理，也不以处理

### **throws** 和 **throw** 有什么区别?

**throws**

1. 用在方法声明后面，跟的是异常类名

2. 可以跟多个异常类名，用逗号隔开

3. 表示抛出异常，由该方法的调用者来处理

4. **throws** 表示出现异常的一种可能性，并不一定发生这些异常

**throw**

1. 用在方法体内，跟的是异常对象名

2. 只能抛出一个异常对象

3. 表示抛出异常，可以由方法体内的语句处理

4. 表示抛出了异常，执行 **throw** 则一定抛出了某种异常

### **finally** 关键字有什么用?

它一般跟着 **try...catch** 一起使用, 放在整个 **try...catch** 的后面

**作用**

1. **try** 中产生异常，并且正常捕获，**finally** 代码块正常执行，之后的代码也正常执行

2. **try** 中没有产生异常，**catch** 异常处理器不执行了，**finally** 代码块仍然正常执行，其后的代码也正常执行

3. **try** 中产生异常，但是没有正常捕获，**jvm** 会终止方法的执行， **try...catch** 之后的代码不执行了，但是 **finally** 仍然执行了

**无论try中什么情况，finally代码块都要执行**

### 当 **try** 当中有 **return** 时会出现什么情况?

1. 如果这个 **return** 在产生异常的代码后面，其实是没啥用，如果在前面，不能这么写

2. 如果 **catch** 中有 **return**, 并且 **catch** 正常执行，那么仍然会执行 **finally** 后再回去 **catch** 中 **return**

3.  **finally** 当中如果有 **return** , **finally** 还会执行

4. 如果 **finally** 和 **catch** 中都有 **return**, 咋办?

### ![20210415190444](https://img.fengqigang.cn//img/20210415190444.png) 如何不执行 **finally** 语句?

**System.exit(0)**

关掉虚拟机

```java
public class demo {
    public static void main(String[] args) {
        try {
            int[] arr = null;
            throw new ArithmeticException();
        } catch (ArithmeticException e) {
            e.printStackTrace();
        } finally {
            System.out.println("finally代码块执行了");
            System.exit(0);
            return;
        }
    }
}
```

### **final**, **finalize**, **finally** 有什么区别?

**final**

修饰符， 修饰 **class** , 方法， 变量 

类: 

不可继承类

方法:

不可重写方法

变量:

变量的值无法修改, 但是不会改变变量在内存中的位置

数据类型:

引用中的地址不变，但是引用的对象仍然可以修改

**finalize**

没用，类似析构函数

**finally**

和 **try...catch** 或者 **try** 一起使用，是一定会执行的代码块, 比起 **fialize** 释放资源，更安全更高效

### 自定义异常有哪几种?

**编译时异常**:

定义一个类， 继承 **Exception**, 就是一个编译时异常

![20210415191831](https://img.fengqigang.cn//img/20210415191831.png)

**运行时异常**:

定义一个类，继承 **RuntimeException**, 就是一个运行时异常

![20210415191840](https://img.fengqigang.cn//img/20210415191840.png)

### 怎么写自定义异常类的构造方法?

直接去调用父类构造器就可以 **super** 参数

### 自定义异常有什么用?

如果直接使用 **jdk** 已有的异常， 比如 **IllegalArgumentException** 这个异常，看起来是可以实现效果的

但是如果 **try** 当中的代码， 本身也会产生这个异常 **IllegalArgumentException** ， 那么就不能区分对待，不能分别处理了

所以自定义异常可以区分自己写的代码的错误，不使用源码中已有的异常，避免混淆


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

### 如何实现 **Data** 的匹配模式?

**SimpleDateFormat** is a concrete class for formatting and parsing dates in a locale-sensitive manner. It allows for formatting (date -> text), parsing (text -> date), and normalization.


**parse** 

Parse a date/time string according to the given parse position

```java
public class Demo {
    public static void main(String[] args) throws IOException, ParseException {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");

        //1. 格式化
        Date d = new Date(3742762088000L);
        String timeStr = sdf.format(d);
        System.out.println(timeStr);

        //2.解析
        String time = "2077/07/07 07:07:07";
        Date parse = sdf.parse(time);
        System.out.println(parse.getTime());

    }
}
```

![20210415210434](https://img.fengqigang.cn//img/20210415210434.png)

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

[20210415214242](https://img.fengqigang.cn//img/20210415214242.png)

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

### 如何计算现在到1970年多少年了? 并返回当时的时间?

**public void setTime(long date)**

Set an existing Date object using the given milliseconds time value.

```java
public class Demo {
    public static void main(String[] args) {
        Date d = new Date();
        long time = d.getTime();
        System.out.println(time / (1000L * 3600 * 24 * 365));

        d.setTime(0);
        System.out.println(d);
    }
}
```

![20210415215456](https://img.fengqigang.cn//img/20210415215456.png)









