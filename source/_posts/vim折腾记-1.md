---
title: vim折腾记-1
date: 2018-09-17 17:29:09
tags: vim
categories: Tools
---

学习 vim 并且其会成为你最后一个使用的文本编辑器。没有比这个更好的文本编辑器了，非常地难学，但是却不可思议地好用。

<!--more-->
## 基本用法

**移动:**
hjkl: 分别对应左下上右

** 切换操作模式**
要始终记得按`esc`来退回Normal模式,已下要说的前提都是在Normal模式开始。

按esc键 → Normal模式，在VIM的Normal模式下，所有的键就是功能键了。

i → insrt模式，相当于其他编辑器正常的输入模式。

: → 后面接命令，进入vim的命令模式。

:! → 调用外部的命令行。

→ 注: 凡是`:`开始的命令你需要输入`<enter>`回车来结束（执行）

## 需要记忆的知识点

**插入**

a → 光标后插入
o → 当前行后插入一行
O → 当前行前插入一行
cw → 替换从光标位置到单词结尾的字符

**位移动**

0 → 到行头
^ → 和0差不多，到本行第一个不是blank字符的位置（blank: 空格、tab、换行、回车等看不见的字符）
$ → 到行尾
g下换线 → 到本行最后一个不是blank字符的位置

**单词间移动**
w → 到下一个单词的开头。
e → 到下一个单词的结尾。

**块内移动**
% : 匹配括号移动，包括 (, {,[

- 和 #:  全局匹配光标当前所在的单词，移动光标到下一个（或上一个）匹配单词（*是下一个，#是上一个)

------

**行移动**
NG → 到第 N 行
gg → 到第一行
G → 到最后一行

**搜索**

/pattern → 搜索`pattern`的字符，如果有多个在enter后 按n 向后，N 先前。

**撤销和取消撤销**

u → undo
<C-r> → redo

**打开/保存/退出/改变文件**
:e <path/to/file> → 打开一个文件
:x/ZZ/:wq → 都是保存并退出
:bn和: bp → 当有多个文件打开时，可以切换 n 是next p是previous

**重复**
. → 重复上一次的命令
N<command> → 重复某个命令N次

如：
2dd → 删除2行
3p → 粘贴文本3次
接着上次按 . 可以再次粘贴文本3次，
但是 3. 则是粘贴文本3次而不是9次

## Vim 超能力

fa → 到下一个为a的字符处，你也可以fs到下一个为s的字符。
t, → 到逗号前的第一个字符。逗号可以变成其它字符。
3fa → 在当前行查找第三个出现的a。
F 和 T → 和 f 和 t 一样，只不过是相反方向。
dt" → 删除所有的内容，直到遇到双引号—— "。



## visual模式下的操作

> 可视选择模式。此时可用hjkl 移动

**选择后的操作**
d → (删除 )
gU → (变大写)
gu → (变小写)
J → 把所有的行连接起来（变成一行）
< 或 > → 左右缩进
= → 自动给缩进

**visual模式的命令**
<action>a<object> 和 <action>i<object>  v模式的命令
action可以是任何的命令，如 d (删除), y (拷贝), v (可以视模式选择)。
object 可能是： w 一个单词， W 一个以空格为分隔的单词， s 一个句字， p 一个段落。也可以是一个特别的字符："、 '、 )、 }、 ]。

假设你有一个字符串 (map (+) ("foo")).而光标键在第一个 o 的位置。

```
vi" → 会选择 foo.
va" → 会选择 "foo".
vi) → 会选择 "foo".
va) → 会选择("foo").
v2i) → 会选择 map (+) ("foo")
v2a) → 会选择 (map (+) ("foo"))
```

**块操作: <C-v>**
块操作，典型的操作： 0 <C-v> <C-d> I-- [ESC]

^ → 到行头
<C-v> → 开始块操作
<C-d> → 向下移动 (你也可以使用hjkl来移动光标，或是使用%，或是别的)
I-- [ESC] → I是插入，插入“--”，按ESC键来为每一行生效。

## 分屏

:vs 水平分屏
:sv 垂直分屏
<C-w>w 顺序切换
<C-w><dir> : dir就是方向，可以是 hjkl 或是 ←↓↑→ 中的一个，其用来切换分屏。
<C-w>_ (或 <C-w>|) : 最大化尺寸 (<C-w>| 垂直分屏)
<C-w>+ (或 <C-w>-) : 增加尺寸

**启动时分屏**

使用大写的O参数来垂直分屏。
`vim -On file1 file2 ...`

> 使用小写的o参数来水平分屏。n 代表分几屏
> **关闭分屏**
> Ctrl+W c

## 自动提示  <C-n> 和 <C-p>

在 Insert 模式下，你可以输入一个词的开头，然后按 <C-p>或是<C-n>，自动补齐功能就出现了……



## 其他

ye 当前位置拷贝到本单词的最后一个字符。
y2/foo 来拷贝2个 “foo” 之间的字符串。
