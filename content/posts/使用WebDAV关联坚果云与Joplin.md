---
title: "使用WebDAV关联坚果云与Joplin"
date: 2021-01-26T22:20:50+08:00
lastmod: 2021-01-26
author: "xiaonan"
math:
 enable: true

tags: [joplin]
categories: [linux]
---

## 关联方法[^关联]
[^关联]:[如何使用WebDAV关联坚果云与Joplin?](https://help.jianguoyun.com/?p=5633)

### 1. 在坚果云上创建一个英文名称的根目录的文件夹, 如"note"

![](https://img.fengqigang.cn//img/20210126220602.png)

### 2. 配置Joplin

![](https://img.fengqigang.cn//img/20210126220807.png)

WebDAV URL: https//dav.jiangguoyun.com/dav/`note`

(note为刚才创建的文件夹名称)

WebDAV 名称: 坚果云账号邮箱

WebDAV 密码: 在坚果云中生成的第三方应用密码[^webdav开启]
[^webdav开启]:[坚果云第三方应用授权WebDAV开启方法](https://help.jianguoyun.com/?p=2064)

### 3. 点击检查"同步配置"

![](https://img.fengqigang.cn//img/20210126221438.png)

### BUG

#### 1. Too many requests are received recently

可以将同步的并发连接数调低(调成1后，等一会, 即可)[^rquests]
[^rquests]: [joplin使用坚果云webdav同步时出现以下问题如何解决？](https://www.zhihu.com/question/398670360/answer/1328037321)

![](https://img.fengqigang.cn//img/20210126221817.png)



