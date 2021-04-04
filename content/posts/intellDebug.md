---
title: "IntellDebug"
date: 2021-04-04T23:40:51+08:00
lastmod: 2021-04-04
author: "xiaonan"
math:
 enable: true

tags: [idea]
categories: [software]
---

## Breakpoints


### Notation

- If a file with breakpoints was modified externally, for example, update through a VCS or changed in an external editor, and the line numbers have changed, **the breakpoints will be moved accordingly**.


### Types of breakpoints(Add breakpoints)

Setting Line breakpoint keymap

![20210404225944](https://img.fengqigang.cn//img/20210404225944.png)

- **Line breakpoints**


Click the gutter at the **executable line of code** or press keymap

![20210404230100](https://img.fengqigang.cn//img/20210404230100.png)

- **Method breakpoints**

Click the gutter at **the line where the method is declared**, or press keymap

![20210404230327](https://img.fengqigang.cn//img/20210404230327.png)

![20210404230613](https://img.fengqigang.cn//img/20210404230613.png)


- **Field watchpoints**

Click the gutter at **the line where the field is declared**, or press keymap

![20210404230856](https://img.fengqigang.cn//img/20210404230856.png)

- **Exception breakpoints**



### Remove breakpoints

- **one breakpoint**

click the breakpoint in the gutter.

![20210404231116](https://img.fengqigang.cn//img/20210404231116.png)

- **all breakpoints**

main menu -> Run -> View Breakpoints -> Select the breakpoint, and click Remove delete.

![20210404232155](https://img.fengqigang.cn//img/20210404232155.png)

![20210404232326](https://img.fengqigang.cn//img/20210404232326.png)

![20210404232438](https://img.fengqigang.cn//img/20210404232438.png)

![20210404232457](https://img.fengqigang.cn//img/20210404232457.png)

#### notation

> To avoid accidentally removing a breakpoint and losing its parameters, you can choose to remove breakpoints by dragging them to the editor or clicking the middle mouse button.

Setting/Preferences -> Build, Execution, Deployment -> Debugger

select **Drag to the editor or click with middle mouse button**

![20210404232928](https://img.fengqigang.cn//img/20210404232928.png)

### Mute breakpoints

> If you don't need to stop at your breakpoints for some time, you can mute them.

![20210404233140](https://img.fengqigang.cn//img/20210404233140.png)

### Enable/disable breakpoints

> To temporarily turn an individual breakpoint off without losing its parameters, you can disable it.

- **onepoint**

**right-click it**

![20210404233522](https://img.fengqigang.cn//img/20210404233522.png)

![20210404233537](https://img.fengqigang.cn//img/20210404233537.png)

**all breakpoint**

![20210404233638](https://img.fengqigang.cn//img/20210404233638.png)

main menu -> Run -> View Breakpoints -> Select the breakpoint, and click Remove delete.

![20210404232155](https://img.fengqigang.cn//img/20210404232155.png)

### Move/copy breakpoints

**Move**

- drag it to another line

**copy**

- hold `Ctrl` and drag a breakpoint to another line


