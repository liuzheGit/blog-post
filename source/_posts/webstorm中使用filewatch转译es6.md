---
title: webstorm中使用filewatch转译es6
date: 2018-11-10 17:37:25
tags: ['JavaScript', 'babel', 'webstrom']
categories: Front-End
---
## 前言

es6的语法也看了不少, 也用了一些, 不过是在vue的vue-cli中直接使用, 不需要自己安装babel. 

可是,有时候自己写个小测试, 不想用框架的cli, 这是就需要自己配置babel了, 也折腾过webpack得loader, 总感觉有问题, 这次就不用webpack, 直接用babel. 是在webstorm中用.

### 操作

1. 全局安装babel-cli , 全局安装 的好处在于 在webstrom中选择filewatch的时候, 不用每次再选择项目中的babel-cli的可执行文件了

   ```shell
   # 最新的babel-core也集成到了babel-cli中,所以还是直接安装吧
   sudo npm i babel-cli -g
   ```

2. 打开webstrom, 新建项目, 然后执行

```shell
npm init -y
npm i -D babel-preset-env 
```

此时都安装好了, 可以选择 webstrom的 preferences -> Tools ->File Watchers 然后点击 `+`号 ,选择 babel, 这里 只需要改动 Program、Arguments 和 Output, 本次 我只是选择了 我自己电脑上的babe-cli的安装路径, 就可用了,  用的是 `babel-preset-env `规则, 其他的没改,目前够我用了.