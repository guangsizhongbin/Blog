---
title: "UltiSnip中的正则"
date: 2021-01-30T22:22:33+08:00
lastmod: 2021-01-30
author: "xiaonan"
math:
 enable: true

tags: [ultisnips]
categories: [nvim]
---

## 1

```
snippet "(\w+).par" "Parenthesis (postfix)" r
(`!p snip.rv = match.group(1)`$1)$0
endsnippet
```

{{< admonition tip >}}
1. `\w+`
匹配`一个或多个`字母、数字、下划线

2. `()`
分组

3. `$0`
结束位置

4. `$1`
结果时光标位置
{{< /admonition >}}

### 2

```
snippet "([^\s].*)\.return" "Return (postfix)" r
return `!p snip.rv = match.group(1)`$0
endsnippet
```

{{< admonition >}}
1. `\s`
匹配所有空白符，包括换行

2. `[^\s]`
除去所有空白符，包括换行
{{< /admonition >}}

### 3

```
snippet t
<tag>${VISUAL:inside text/should/is/g}</tag>
endsnippet
```

{{< admonition >}}
1. `${VISUAL}`
The syntax is:

${VISUAL:default/search/replace/option}
{{< /admonition >}}

### 4

```
snippet "be(gin)?( (\S+))?" "begin{} / end{}" br
\begin{${1:`!p
snip.rv = match.group(3) if match.group(2) is not None else "something"`}}
	${2:${VISUAL}}
\end{$1}$0
endsnippet
```

{{< admonition >}}
1. `?`
表示匹配前面的子表达式零次或一次

2. `be(gin)?`
可以匹配 be, beg, begi, begin

3. `\S`
匹配任何非空白字符

4. `\S+`
匹配一个或多个非空白字符
{{< /admonition >}}



### 参考文章

[正则表达式 - 语法](https://www.runoob.com/regexp/regexp-syntax.html)

[UltiSnips.txt](https://github.com/SirVer/ultisnips/blob/master/doc/UltiSnips.txt)




