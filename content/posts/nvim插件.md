---
title: "Nvim插件"
date: 2021-01-27T22:47:15+08:00
lastmod: 2021-01-27
author: "xiaonan"
math:
 enable: true

tags: [nvim]
categories: [nvim]
---

## Markdown[^markdown]
[^markdown]: [vim-markdown](https://github.com/plasticboy/vim-markdown/issues?q=is%3Aissue+is%3Aopen+vim-plug)

```
Plug 'godlygeek/tabular' "必要插件
Plug 'plasticboy/vim-markdown'

" To disable math conceal with LaTex math syntax enabled, add the following
let g:tex_conceal = ""
let g:vim_markdown_math = 1
```

- `[[`: go to previous header.

- `]]`: go to next header.

- `]c`: go to Current header.

- `]u`: go to parent header (Up).

- `zR`: opens all flods

- `zM`: folds everything all the way

- `zr`: reduces fold level throughout the buffer

- `zm`: increases fold level throughout the buffer

## snippets[^snippets]
[^snippets]: [高效做笔记:vim + markdown](https://github.com/cold-soda-jay/Markdown-vim)

### `UltisnipsEdit`进入编辑页面[^Edit]
[^Edit]: [UltiSnips Screencast Episode 2](https://www.sirver.net/blog/2012/01/08/second-episode-of-ultisnips-screencast/)

```
snippet triggerWord "Comment" iAwrb
your snippets
endsnippet
```

`triggerWord` 为关键词

`iAwrb`为snippet的选项
	- i 表示片段可在句中被触发
	- A 表示片段会被自动出发
	- w 表示片段会在关键词为单独单词的情况下被触发
	- r 表示关键词语使用正则表达式, 正则表达式必须用两个引号''包围
	- b 表示只有在一行的开头才会被触发

#### 数学模式下自动加下标

```
snippet '([A-Za-z])(\d)' "auto subscript" wrA
`!p snip.rv = match.group(1)`_`!p snip.rv = match.group(2)`
endsnippet
```

{{< admonition >}}
- `[A-Za-z]`: 匹配A-Z, a-z

- python代码
		- `fn` 表示当前文件名
		- `path` 当前文件名的路径
		- `t` 占位符的字典, 可以用`t[1], t[2], t.v`来取占位符内容
		- `snip.rv` 表示 return value
		- `snip.fn` 表示当前文件名
		- `snip.ft` 表示当前文件类型
		- `snip.v` 表示VISUAL模式变量
		- `snip.v.mode` 表示模式类型
		- `snip.v.text` 表示VISUAL模式中选择的字符

- 占位符选择
		- `/<tab>` 切换下一个占位符
		- `<shift-tab>` 切换上一个占位符
{{< /admonition >}}

#### 创建表格

```
snippet '(?<!\\)([0-9])([0-9])tb' "new table" r
$1`!p 
x=match.group(1)
y=match.group(2)
row1=""
row2="" 
for i in range(int(x)):
	row1+="| "
	row2+="|:-:"
row1+="|\n"
row2+="|\n"
out=row1+row2+int(y)*row1
snip.rv=out
`$0
endsnippet
```


```
# 若输入 ‘/’，则检查符号前的字符是否为数字或者字母，
# 将数字或字母作为分子扩展为Latex分数形式然后在分母部分等待输入
priority 100
snippet '((\d+)|(\d*)(\\)?([A-Za-z]+)((\^|_)(\{\d+\}|\d))*)/' "Fraction" wrA
\\frac{`!p snip.rv = match.group(1)`}{$1}$0
endsnippet

snippet talk "something"
Talk is ${1:cheap}, show me the ${2:code} $0
endsnippet

# code
snippet code "code"
\`\`\` ${1:language}
${2:code}
\`\`\`
$0
endsnippet

# more
snippet more "more"
<!--more-->
endsnippet

# admonition
snippet ad "admonition"
{{< admonition >}}
${1:admonition}
{{< /admonition >}}
$0
endsnippet

# link
snippet link "link"
[${1:name}](${2:link})
$0
endsnippet

# picture
snippet pic "pic link"
![${1:name}](${2:link})
$0
endsnippet
```
