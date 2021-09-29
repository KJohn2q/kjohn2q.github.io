---
title: vim cheatsheet
tags:
  - vim
  - linux
  - cheatsheet
categories: 笔记
date: 2021-09-29 00:00:00
---


> vim是一个可高度定制的文本编辑器，使得创建和修改文件更加高效。

## 设计哲学

`vim` 设计的目的就是为了摆脱鼠标，所有工作都可以通过键盘完成。为了提高效率，需要使得双手尽可能少的移动位置。

![illustration of a keyboard with home row keys](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202109291548160.png)

![](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202109291124231.png)

##  模式

`vim` 中有四种模式：普通模式，编辑模式，命令模式和视图模式。

### 普通模式

`vim` 默认为普通模式。在普通模式中我们可以进行光标的移动，文本的复制、粘贴和删除。

#### 取代方向键

`h` 光标向左移动

`j`  光标向下移动

`k` 光标向上移动

`l` 光标向右移动

#### 光标水平移动

`w/W` 移动到下一个单词 （word）,  word 默认为一个序列，包含字符，数字或者下划线

`b/B` 移动到上一个单词 （word）

`0` 移动到当前行的开头

`^` 移动到当前行的第一个不为空格的字符前

`$` 移动到当前行的末尾

`%` 如光标在一个花括号的开头，则会移动到匹配的花括号另一半的位置

> If operators are the verbs, text objects are the nouns. Simply put, a text object is a set of character. In Vim, a `word` is a text object, as well as a `sentence` or a `paragraph`.    ——  [Is Vim Really Not For You? A Beginner Guide ](https://thevaluable.dev/vim-beginner/)

#####  移动到指定字符的位置

`f[character]`  在当前光标之后查找字符，并移动   `f`: `find`

`F[character]`  在当前光标之前查找字符，并移动

`t[character]`  移动到当前光标之后指定字符的位置  `t`:  `to`

`T[character]`  移动到当前光标之前指定字符的位置 

在使用了上面的四个操作后，可以使用 `;` 向前移动到下一次出现的位置， 使用`,` 移动到上一次出现的位置。

#### 光标垂直移动

`<line_number>G`  移动到指定的行，如 `10G` , 则移动到第10行

`G`  移动到文件的最后一行

`1G` 或  `gg`   移动到文件的第一行 

##### 快捷键

`ctrl+e`   窗口向下滚动

`ctrl+u`  光标向上滚动半屏  `u`: `upward`

`ctrl+d`  光标向下滚动半屏  `d`: `downward`

####  其它指令

`u`    撤销上一次编辑

`r` 或 `ctrl+r`  重新编辑当前字符  

`d`    删除

`dd`  删除当前行

`[number]dd`  删除包含当前行在内的 `number` 行内容

`c`    修改

`y`    复制

`yy`  复制当前行

`[number]yy`  复制包含当前行在内的 `number` 行内容

`p/P`  粘贴

#### 混合使用

`d$`  删除从光标位置到当前行末尾的所有字符

`dgg`  删除从文件开头到光标位置的内容

`ggdG`  删除文件的所有内容

`diw`   删除光标所在位置的 `word`

`ciw`  删除光标所在位置的 `word`  , 并进入编辑模式

`dip`   删除光标所在位置的 段落

#### 搜索

键入`/[keyword]`  后回车可在本文档中搜索指定的关键词 ，键入 `n` 可以跳转到下一个结果的位置，键入 `N` 可以跳转到上一个结果的位置

普通模式下也可以使用  `*`  来向后搜索当前词汇, 键入 `#` 向前搜索当前词汇

### 编辑模式

在普通模式下，输入 `i` 可在当前字符前进入编辑模式。编辑模式可随意删除，添加和修改内容

`a`  在当前字符后插入内容，进入编辑模式

`A`   光标移动至当前行末尾，进入编辑模式

`o`  在当前行下新起一行，进入编辑模式

`O`  在当前行上插入一行，进入编辑模式

编辑模式下，`esc` 或  `ctrl+c` 或  `ctrl+[` 可回到普通模式

### 命令模式

普通模式下，可键入 `:`进入命令模式。此时光标会自动移动到左下角，可以键入想要的命令。

![image-20210929170014833](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202109291700025.png)

下面列举一些基础命令：

* `:help`  打开 `vim` 的帮助文档。如：如果你不知道如何退出，你可以通过键入 `:help quit` 来获取帮助
* `:q`  退出当前窗口。如果仅有一个窗口，将会退出 `vim`
* `:q!`  不保存就退出。
* `:w`    保存当前文件
* `:wq`  或 `:x`  保存并退出
*  `:e <path>`  编辑指定的文件， `path` 可以是绝对路径或相对路径。  

#### 一些有用的帮助命令

* `:help helphelp`
* `:help vim-modes`
* `:help insert.txt`
* `:help visual.txt`
* `:help cmdline.txt`
* `help write-quite`
* `:help ex-cmd-index`
* `:help search-commands`
* `:help undo-redo`
* `:help cursor-motions`
* `:help left-right-motions`
* `:help up-down-motions`
* `:help scrolling`
* `:help operator`
* `:help text-objects`
* `:help options`
* `:help option-list`

### 可视化模式

可视化模式主要用来选中内容。该模式下，可以修改，复制选中的内容。普通模式下可通过键入 `v` 进入可视化模式，此时在左下角可以看到 `--VISUAL--` 标识：

![image-20210929171256138](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202109291712270.png)

同样的，我们可以通过 `esc` 或 `ctrl+c` 返回到普通模式。

#### 快捷操作

普通模式下，我们可以通过 `shift+v` 进入可视化模式，并选中当前行

![image-20210929171750276](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202109291717546.png)

普通模式下，可以通过 `ctrl+v` 进入可视化模式，并选中当前段落

## 引用

*  [Is Vim Really Not For You? A Beginner Guide (thevaluable.dev)](https://thevaluable.dev/vim-beginner/)