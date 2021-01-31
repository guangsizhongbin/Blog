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

### 5

```
global !p
def upper_right(inp):
	return (75 - 2 * len(inp))* ' ' + inp.upper()
endglobal

snippet wow
${1:Text}`!p snip.rv = upper_right(t[1])`
endsnippet
```

{{< admonition >}}
1. `75 - 2 * len(inp)`

![](https://img.fengqigang.cn//img/20210131094547.png)


{{< /admonition >}}

### 6

``` 
snippet letter
Dear $1,
$0
Yours sincerely,
$2
endsnippet
```

{{< admonition >}}
1. `$0`
It is always the last tabstop in the snippet no matter how many tabstops are defined.
{{< /admonition >}}


### 7. choice tabstop

```
snippet q
Your age: ${1|<18,18~60,>60|}
Your height: ${2|<120cm,120cm~180cm,>180cm|}
endsnippet
```

{{< admonition >}}
`${1|item1, item2, item3, ...|}`
{{< /admonition >}}

### 8. mirrors

```
snippet env
\begi{${1:enumerate}}
	$0
\end{$1}
endsnippet
```
### 9. Transformations

{{< admonition >}}
{<tab_stop_no/regular_expression/replacement/options}

The components are defined as follows:
|components | defined|
|:-:|:-:|
|tab_stop_no | The number of the tabstop to reference|
|regular_expression | The regular expression the value of the referenced tabstop is matched on|
|replacement |The replacement string, explained in detail below |
|options | Options for the regular expression|

The options can be any combination of
| options|combination |
|:-:|:-:|
| g|global replace |
|i | case insensitive|
|m | multiline|
|a | ascii conversion|
{{< /admonition >}}

```
snippet title "Title transformation"
${1:a text}
${1/\w+\s*/\u$0/}
endsnippet
```

{{< admonition >}}
`\w+` 匹配一个或多个字母、数字、下划线

`\s*` 匹配零个或多个任何空白字符

`\u` Uppercase next letter
{{< /admonition >}}

```
snippet title "Title transformation"
${1:a text}
${1/\w+\s*/\u$0/g}
endsnippet
```

{{< admonition >}}
- `g` 
		- blobal replace
			By default, only the first match of the regular expression is replaced. With this option allmatches are replaced.
{{< /admonition >}}





### 参考文章

[正则表达式 - 语法](https://www.runoob.com/regexp/regexp-syntax.html)

[UltiSnips.txt](https://github.com/SirVer/ultisnips/blob/master/doc/UltiSnips.txt)




