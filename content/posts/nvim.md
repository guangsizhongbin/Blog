---
title: "Nvim"
date: 2021-01-21T17:36:39+08:00
lastmod: 2021-01-21
author: "xiaonan"
math:
 enable: true

tags: [Nvim]
categories: [archlinux]
---

## 自动安装vim-plug[^junegunn/vim-plug]
[^junegunn/vim-plug]:[junegunn/vim-plug](https://github.com/junegunn/vim-plug/wiki/tips#automatic-installation)

```
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.vim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall --sync | source $MYVIMRC
endif
```

{{< admonition >}}
> 1. `$MYVIMRC`

The `$MYVIMRC` environment variable is set to the file that was first found, unless `$MYVIMRC` was already set and when using VIMINIT.
{{< /admonition >}}

## 基本配置

### 行相关配置

```
set number
set relativenumber
set cursorline
set tabstop=2
set shiftwidth=2
set softtabstop=2
```

{{< admonition >}}
What is the difference between `tabstop`, `shiftwidth`, `expandtab`, `softtabstop`?

[^Tab settings in Vim]
[^Tab settings in Vim]: [Tab settings in Vim](https://arisweedler.medium.com/tab-settings-in-vim-1ea0863c5990#:~:text=tabstop%20is%20effectively%20how%20many,a%20backspace%20keypress%20is%20worth.)
> 1. `tabstop`
effectively how many columns of whitespace a `\t` is worth

> 2. `shiftwidth`
how many colums of whitespace a "level of identation" is worth

> 3. `expandtab`
Setting `expandtab` means that you never wanna see a `\t` again in your file

> 4. `softtabtop`
how many columns of whitespace a `tab` keypress or a `backspace` keypress is worth
{{< /admonition >}}


#### swap, backup, undo Files 配置[^Vim: Remove swap, backup and undo Files from Working Directory]
[^Vim: Remove swap, backup and undo Files from Working Directory]:[Vim: Remove swap, backup and undo Files from Working Directory](https://medium.com/@Aenon/vim-swap-backup-undo-git-2bf353caa02f)

```
silent !mkdir -p ~/.config/nvim/tmp/backup
silent !mkdir -p ~/.config/nvim/tmp/undo

set backupdir=~/.config/nvim/tmp/backup,.
set directory=~/.config/nvim/tmp/backup,.
```


{{< admonition >}}
1. Swap file
`.myfile.txt.swp` is a `swap file`, containg the unsaved changes.

2. Backup file
`myfile.txt`` is a backup file -- the version of `myfile.txt` before your edited it.

3. Undo file
`.myfile.txt.un`` is an undo file, containing the undo trees of the file edited.

4. directory
List of directory names for the swap file, separated with commas.
{{< /admonition >}}

#### updatetime 
If this many milliseconds nothing is type the swap file will be written to disk（default 4000）

#### colorcolumn
`colorcolum` is a comma separated list of screen columns that are highlighted with ColorColumn hl-ColorColumn.

### Basic Mappings

#### `<LEADER>`
`let mapleader=" "`

{{< admonition >}}
`let {var-name} = {expr1}`
Set internal variable `{var-name}` to the result of the expression `{expr1}`. The variable will get the type from the `{expr}`. If `{var-name}` didn't exist yet, it is created.
{{< /admonition >}}

#### Save & quit

```
noremap Q :q<CR>
noremap <C-q> :qa<CR>
noremap S :w<CR>
```

{{< admonition >}}
`noremap {lhs} {rhs}`
Map the key sequence `{lhs}` to `{rhs}` for the modes where the map command applies. Disallow mapping of `{rhs}`, to avoid nested and `recursive` mappings. 
{{< /admonition >}}

##### What is the difference between the `remap`, `noremap`, `nnoremap` and `vnoremap` mapping commands in Vim? [^What is the difference between the remap, noremap, nnoremap and vnoremap mapping commands in Vim?]
[^What is the difference between the remap, noremap, nnoremap and vnoremap mapping commands in Vim?]: [What is the difference between the remap, noremap, nnoremap and vnoremap mapping commands in Vim?](https://stackoverflow.com/questions/3776117/what-is-the-difference-between-the-remap-noremap-nnoremap-and-vnoremap-mapping)

`remap` is an option that makes mappings work recursively.

`:map` and `:noremap` are recursive and non-recursive versions of the various mapping commands.

```
:map j gg				(moves cursor to first line)
:map Q j				(moves cursor to first line)
:noremap w j		(moves cursor to down one line)
```

- `j` will be mapped to `gg`.

- `Q` will also be mapped to `gg`, because `j` will be expanded for the recursive mapping.

- `W` will be mapped to `j` (and not to `gg`) because `j` will not be expanded for the non-recursive mapping.

normal modes: `:map` and `:nnoremap`

visual modes: `:vmap` and `:vnoremap`

Select modes: `:smap` adn `:snoremap`


#### Open the vimrc file in anytime

```
noremap <LEADER> :e ~/.config/nvim/init.vim<CR>
```

#### copy content

```
" make Y to copy till the end of the line
nnoremap Y y$

" Copy to system clipboard
vnoremap Y "+y
```

#### Search
```
set ignorecase
set smartcase
noremap <LEADER><CR> :nohlsearch<CR>
```

#### scrolloff
```
set scrolloff=4
```

{{< admonition >}}
`scrolloff`:

Minimal number of screen lines to keep above and below the cursor. This will make some context visible around where you are working.
{{< /admonition >}}


#### Resize splits
```
noremap <up> :res +5<CR>
noremap <down> :res -5<CR>
noremap <left> :vertical resize -5<CR>
noremap <right> :vertical resize +5<CR>
```

#### Markdowm Setting

```
noremap <LEADER><LEADER> <Esc>/<++><CR>:nohlsearch<CR>c4l
autocmd Filetype markdown inoremap <buffer> ,f <Esc>/<++><CR>:nohlsearch<CR>"_c4l
autocmd Filetype markdown inoremap <buffer> ,w <Esc>/ <++><CR>:nohlsearch<CR>"_c5l<CR>
autocmd Filetype markdown inoremap <buffer> ,m <!--more--><CR>
autocmd Filetype markdown inoremap <buffer> ,a {{< admonition >}}<CR><++><CR>{{ /admonition }}<CR><++><Esc>
autocmd Filetype markdown inoremap <buffer> ,c \```<Enter><++><Enter>```<Enter><Enter><++><Esc>4kA
autocmd Filetype markdown inoremap <buffer> ,l [](<++>) <++><Esc>F[a
autocmd Filetype markdown inoremap <buffer> ,p ![](<++>) <++><Esc>F[a
```

{{< admonition tip  >}}

> `_`

1 lines downward, on the first non-blank

> `["x]c{motion}`

Delete `{motion}` text [into register x] adn start insert.

> `l`
`[count]` characters to the right.

> `f{char}`
To `[count]`'th occurrence of `{char}` to the right.

> `F{char}`
To the `[count]`'th occurrence of `{char}` to the right.

> `"`
Use register {a-zA-Z0-9.%#:-"} for next delete, yank or put (use uppercase character to append with delete and yank) ({.%#:} only work with put)

{{< /admonition >}}



