---
title: webpack学习byjrg
date: 2018-09-26 20:28:12
tags: webpack
categories: Front-End
---

# Webpack

我学新东西的套路就是：
「copy - run - modify」
「抄 - 运行 - 修改」

1. 抄文档给的例子
2. 在自己这里运行成功
3. 改一下，看还能不能运行成功

我们学 Webpack 也遵循同样的套路。

# 安装

我们要使用 npm 来安装 webpack。

1. 为了让你更了解 npm，我们要做两件事（可不做）

   1. 运行 `npm config set loglevel http`，让你知道 npm 发的每一个请求
   2. 运行 `npm config set progress false`，关闭那个进度条

2. 为了让你的安装速度变快，运行

    

   ```
   npm config set registry https://registry.npm.taobao.org/
   ```

   1. 这会让你在运行 npm adduser 的时候出问题，想要恢复成原样，只需要 `npm config delete registry` 即可

3. 现在，使用

    

   ```
   npm i -g webpack
   ```

   ，正式安装 webpack

   1. 如果报错说有权限问题，就是用 `sudo npm i -g webpack`
   2. Windows 里没有 sudo，那么你只能「以管理员身份运行」Git Bash，然后再运行命令

4. 验证安装成功

   运行

    

   ```
   webpack --help
   ```

    

   如果看到类似下面的信息，就说明安装成功

   ```
   webpack 1.14.0
   Usage: https://webpack.github.io/docs/cli.html
   ...
   ...
   --display-cached-assets
   --display-reasons, --verbose, -v
   ```

# ES Modules

终于安装好了，可以开始使用 Webpack 了吗？

不行，我们有一个重要的知识需要学习一下，那就是 ES 模块，也就是 import 和 export 两个关键字。

请现到 MDN 上了解一下它们的用法：

[import 用法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/import)

[export 用法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/export)

如果你看晕了，没关系，你只要看两个页面的最前面一段就行了。后面我们会用 「copy - run - modify」 套路来学习它们。

# Webpack

## copy：去 Webpack 的官网上找个例子来玩玩

<https://webpack.js.org/>

往下滚，看到例子

## run：把例子弄到本地

1. 随意建个目录，比如 webpack-demo

2. 进入目录后，将官网的例子弄到本地，结果如下：

   ```
   .
   ├── app.js
   ├── bar.js
   ├── page.html
   └── webpack.config.js
   ```

3. 按照官网说的，运行

    

   ```
   webpack
   ```

   ，看到如下结果：

   ```
   Hash: a5d289a022d184d8fbff
   Version: webpack 1.14.0
   Time: 36ms
       Asset     Size  Chunks             Chunk Names
   bundle.js  1.42 kB       0  [emitted]  main
      [0] ./app.js 33 bytes {0} [built]
   ```

4. 打开 page.html，F12 打开控制台，居然报错了！！！

   ```
   Uncaught SyntaxError: Unexpected token import
   ```

   不靠谱的官网

5. 然后只能 copy

    

   阮一峰的教程

   咯，把 webpack.config.js 改成这样

   ```
   module.exports = {
     entry: './app.js',
     output: {
       filename: 'bundle.js'
     },
     module: {
       loaders:[
         {
           test: /\.js[x]?$/,
           exclude: /node_modules/,
           loader: 'babel-loader?presets[]=es2015&presets[]=react'
         },
       ]
     }
   }
   ```

6. 再次运行

    

   ```
   webpack
   ```

   ，又出错：

   ```
   ERROR in Entry module not found: Error: Cannot resolve module 'babel-loader' in /tmp/webpack-demo
   ```

   是阮的问题吗？不是，他的教程里说了要安装一些 npm 包才能成功。

   上面的提示说没有 'babel-loader' ，我们试着安装一下：

   ```
   npm i babel-loader
   ```

   再次运行

    

   ```
   webpack
   ```

   ，它说需要安装 'babel-core'，跟上次的提示不一样了，看来只要我们一直安装下去就行了

   ```
   npm i babel-core
   ```

   再运行

    

   ```
   webpack
   ```

   ，提示变了：

   ```
   Module build failed: Error: Couldn't find preset "es2015" relative to directory "/tmp/webpack-demo"
   ```

   这次需要安装的是

    

   ```
   babel-preset-es2015
   ```

   （不要问我为什么它不提示完整的名字）

   ```
   npm i babel-preset-es2015
   然后运行 webpack，看报错，知道需要安装 babel-preset-react
   npm i babel-preset-react
   然后运行 webpack，终于成功了……
   Hash: 4950c10e0d1d81a2a8f1
   Version: webpack 1.14.0
   Time: 475ms
       Asset     Size  Chunks             Chunk Names
   bundle.js  1.83 kB       0  [emitted]  main
       + 2 hidden modules
   ```

7. 用浏览器打开 page.html，F12 打开控制台，终于没有报错了！

## Modify

虽然没有报错，但是什么功能也没有啊！摔！再次吐槽 Webpack 官网。

我们来改一下 bar.js 吧：

```
export default function bar() {
  alert('Hello Webpack!')
}
```

重新运行 webpack，然后刷新 page.html。

如果你看到浏览器弹框说「Hello Webpack」，那么你就学会使用 Webpack 了。

# 致饥人谷学员

你需要看懂这篇教程，并且运行成功。

然后新建一个 GitHub 项目，将代码上传到里面。上传成功后，将项目主页的链接放在本帖的评论区中，谢谢！

## 注意

你需要在项目的根目录添加 .gitignore 文件，并且在里面加上一行 `node_modules`，以防止你把这个目录上传到 GitHub 上。你在新建项目的时候选择 Node，也可以达到同样目的。

但是缺点就是我无法使用你安装的 npm 包，所以你需要把你安装的包写在一个地方，比如 README 里：

```
npm i babel-loader babel-core babel-preset-es2015 babel-preset-react
```

当然你用 package.json 来记录就更好了
