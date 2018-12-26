---
title: vim优化-语法学习
date: 2018-10-22 21:03:09
tags: vim
categories: Front-End
---

vimrc 是控制 vim 行为的配置文件，位于 ~/.vimrc，不论 vim 窗口外观、显示字体，还是操作方式、快捷键、插件属性均可通过编辑该配置文件将 vim 调教成最适合你的编辑器。

## 快捷键修改

>  想要修改快捷键，必须了解vim的键映射map，它有五种前缀，对应着vim中的五种模式：

```
nore前缀： 非递归
 
n前缀：    在普通模式下生效
 
v前缀：    在可视模式下生效
 
i前缀：     在插入模式下生效
 
c前缀：    在EX命令模式下生效
```

通过不同的前缀，就能明确告诉vim，我们自定义的快捷键在哪种模式下生效。

除此之外，还要配合键表：

<k0>-<k9>       小键盘数字0到9

<S-x>                大写S配合x，意味着shift+x组合键

<C-x>               大写C配合x，意味着ctrl+x组合键

<A-x>               大写A配合x，意味着alt+x组合键

<ESC>               ESC键

<BS>                backspace退格键


<CR>                ENTER回车键


<Space>           空格键


<Shift>             shift键


<Ctrl>               ctrl键


<Alt>                alt键


<F1>-<F12>    F1到F12功能键

尽管能映射的键表非常丰富，但因为某些历史原因，ALT几乎无法映射。

同时CTRL键被系统频繁使用，F1到F12功能键某些也被vim占用。

比如F1是帮助，这些都不适合用来映射，以免造成快捷键冲突。



更改键盘默认按键时要特别注意, 不用递归

```vim
// 例子
nnoremap  i   k
nnoremap  k  j
nnoremap  j   h
```

此时使用的是前缀n ,表示在normal模式下生效,

使用前缀nore,表示不递归,否则按下i等于按下k,就等于按下j, 等等就乱套了.

## 功能映射

> vim自带的行光标移动也不方便，移动到行首^，需要按shift+6，移动到行尾$，需要按shift+4。

个人也把它们进行映射：

```undefined
"行光标移动
nmap lh   ^
nmap le   $
```

连续按下lh就表明移动到行首，lh可以理解成line_head，le理解成line_end.

具体用什么样的快捷键映射不重要，重要的是能不能方便自己使用与记忆。

我们可能需要频繁变更 .vimrc，要让变更内容生效，一般的做法是先保存 .vimrc 再重启 vim，太繁琐了。

增加如下设置，可以实现在保存 .vimrc 时自动重启加载它。

```
" 让配置变更立即生效
autocmd BufWritePost $MYVIMRC source $MYVIMRC
```

## <leader>前缀键

> vim自带的快捷键很多，再加上各类插件提供的快捷键，我们自己定义的快捷键，这些混合在一起，非常容易引起按键的冲突，为了环境该问题，vim引入了<leader>前缀键。

前缀键的意思就是，在各种快捷键的最前面加上<leader>，避免了二义性。

比如我们定义<leader>是`,`号:

```
let mapleader=','
"配合键盘映射
nmap <leader>w   :w<CR>
```

在普通模式按下#w时，就完成了文件的保存工作。

当然，最好还是把所有映射都设定为普通模式下有效，尽管在完成结果上没有什么区别，但违背了vim设定几种模式的本意，插入模式仅用来输入字符，功能都放进普通模式或者EX命令模式。

作者：dark_tone 
原文：https://blog.csdn.net/dark_tone/article/details/52856032 

