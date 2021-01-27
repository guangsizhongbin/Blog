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

