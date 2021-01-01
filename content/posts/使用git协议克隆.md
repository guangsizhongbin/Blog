---
title: "使用git协议克隆"
date: 2021-01-01
lastmod: 2021-01-01
author: "xiaonan"

tags: [git]
categories: [git]

---

## 使用`git`协议克隆的好处

1. 配置完后，每次提交均不需要输入账号密码

## 如何配置

1. 创建一个SSH Key

```bash
$ ssh-keygen -t rsa -C "guangsizhongbin@gmail.com"
```

参数含义：
- -t
	- Specifies the type of key to create.
- -C 
	- Provides a new comment.

```bash
Enter file in which to save the key (/home/feng/.ssh/id_rsa):
```

参数含义：
- -f filename
	- Specifies the filename of the key file.
指定生成文件的文件名（文件路径，否则会直接生成在当前目录下）

---
例如:

```bash
ssh-keygen -t rsa -C "guangsizhongbin@gmail.com" -f a
```

> 会在当前路径下生成私钥`a`, 公钥`a.pub`
---

```bash
Enter passphrase (empty for no passphrase):
 
Enter same passphrase again:
```

- passphrase:
	- a sequence of words used to gain access to a computer system

填写`push`文件时需要输入的密码

2. 将`公钥id_ras.pub`传至`github`中（默认路径`.ssh/id_ras.pub`）

`bash`:

```bash
cat .ssh/id_rsa.pub
```

`github`:

Repositories -> Settings -> Deploy keys -> Add deploy key -> Add key

![](https://img.fengqigang.cn//img/20210101150334.png)

![](https://img.fengqigang.cn//img/20210101150550.png)

若要有`push`权限必须要勾选`Allow write access`, 否则只有`read` 权限

![](https://img.fengqigang.cn//img/20210101154712.png)




3. 测试`SSH key`

```bash
ssh -T git@github.com
```

```
The authenticity of host 'github.com (192.30.255.112)' can't be established.RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/\[fingerprint\])? yes
Warning: Permanently added 'github.com,192.30.255.112' (RSA) to the list of known hosts.
Enter passphrase for key '/home/feng/.ssh/id\_rsa':
```

输入创建`SSH key`的时候设置的密码(若有设置)

```
Hi guangsizhongbin/Blog! You've successfully authenticated, but GitHub does not provide shell access.
```
此时已经设置成功了

4. 使用git协议进行克隆

![](https://img.fengqigang.cn//img/20210101151055.png)

```bash
git clone git clone git@github.com:guangsizhongbin/Blog.git

Cloning into 'Blog'...
Enter passphrase for key '/home/feng/.ssh/id_rsa':
```

输入创建`SSH key`的时候设置的密码(若有设置)

## 参考文章
[1. github设置添加SSH](https://www.cnblogs.com/ayseeing/p/3572582.html)
