---
title: scp命令-每天一个linux命令
date: 2018-12-04 17:28:00
tags: linux
categories: Back-End
---

## 介绍

linux 的 scp 命令是用来在linux间安全的复制文件和目录.
scp: 是 `secure copy` 的缩写, 是基于`ssh`登录进行安全的远程文件拷贝命令.

## 语法

`scp [参数] file_source file_target`


**参数说明(常用)**

- `-r`： 递归复制整个目录
- `-v`：详细方式显示输出
- `-P port`：注意是大写的P, port是指定数据传输用到的端口号
- `-p`：保留原文件的修改时间，访问时间和访问权限
- `-C`: 允许压缩。（将-C标志传递给ssh，从而打开压缩功能）

例如: 

`scp -r ./file/ username@ip ./targetFile/`

## 实例

1. 本地复制到远程:

```shell
    # 文件
    scp ./temp/foo.js root@aiminn.top:foo  #这个是复制到foo文件夹内,名称不变
    scp ./temp/foo.js root@aimnnn.top:foo/bar.js  #改名为bar.js

    # 文件夹
    scp -r ./temp/ root@aiminn.top:foo
```

2. 远程复制到本地

```shell
    scp root@aiminn.top:home/index.html ./home/
    scp -r root@aiminn.top:home/ ./home
```
