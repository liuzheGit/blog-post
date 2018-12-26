---
title: Mac下如何安装Exuberant Ctags
date: 2018-09-28 18:04:36
tags: [Mac, Ctags]
categories: Front-End
---

## 安装

```shell
brew install ctags-exuberant
```

安装完后，使用 which -a ctags，如果出现

```shell
/usr/bin/ctags ==> original ctags

/usr/local/bin/ctags ==> exuberant ctags
```

则安装没出啥问题,但是此时系统用的是默认xcode里的`ctags`，而不是我们要使用的
`exuberant ctags`


打开~/根目录下的.profile，如果你也没发现有这个文件，没关系，创建一个！
然后在里面添加：export PATH="/usr/local/bin:/usr/local/sbin:$PATH"
再到终端执行：source ~/.profile
然后再看看which ctags，如无意外，应该是/usr/local/bin/ctags


最后在.vimrc配置文件添加： let Tlist_Ctags_Cmd="/usr/local/bin/ctags"
