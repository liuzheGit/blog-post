---
title: 用node-sass来转译scss文件
date: 2018-12-13 13:49:28
tags: [css, scss]
categories: Front-End
---

#用node-sass来转译scss文件

sass是来之ruby社区的。 所以想要用 sass 需要安装ruby。 但是我不做 ruby的开发， 不想要安装 ruby 。 

**解决办法**： 

Nodejs 的 node-sass 就是来做这样的事的。

安装 之前需要 配置一下 源 。不然 `npm i node-sass`的时候 会报错 ：

配置： 在你的 bash配置中(~/.bashrc 或 ~/.zshrc) 添加 

`export SASS_BINARY_SITE="https://npm.taobao.org/mirrors/node-sass"`

这样 就会用淘宝的源安装 node-sass



### 项目中 安装 node-sass

```sh
npm init -y
npm i -D node-sass
```

然后再`package.json`中 配置` script`来运行 node-sass ， 

也可以直接 使用 npx node-sass ...



### 在全局安装 node-sass 错误解决

>  mac os 系统下需要加 `sudo` 

`sudo npm i -D node-sass -g`

此时 报了错误, 大意还是说 权限不够, 然后到去 找 解决方法: 在百度搜了一大圈发现 全是教配置 淘宝源的, 没有我想要.  只能去google了, 到了 github上 找到node-sass 夏目的 指导页面, 全是英文, 硬着头皮看吧, 终于让我找到了.

 **意思是说:**

如果 你用的是linux 或者 macos系统 , 全局安装`node-sass`就算你使用 sudo , 但还是会有一个npm的安全功能给阻止, (您应该始终避免运行`npm`，`sudo`因为安装脚本可能是无意的恶意)但是 如果你必须要用 的话 需要使用 `--unsafe-perm` 来解决报错:

`$ sudo npm install --unsafe-perm -g node-sass`

这样就可以 直接 node-sass 来在所有项目中使用了.

 [github](https://github.com/sass/node-sass/blob/master/TROUBLESHOOTING.md#linuxosx)寻找答案





### 用法： 

```sh
node-sass src/style.scss dist/style.css
```





###参数

- `-w` 监听文件改动

- `-r` 递归的监听目录

- `--output-style` 指定代码编译风格 

  - ```
    * nested：嵌套缩进的css代码，它是默认值。
    
    * expanded：没有缩进的、扩展的css代码。 (最直观的)
    
    * compact：简洁格式的css代码。 (一行一个)
    
    * compressed：压缩后的css代码。 (只有一行)
    
    # 生产环境当中，一般使用最后一个选项。
    ```

  - 