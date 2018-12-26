---
title: webpack中babel-loader的配置过程
date: 2018-10-25 16:31:13
tags: [webpack,JavaScript]
categories: Front-End
---
## 真理: 官网才是王道

### 回合1

> 此次的是在网上看的blog做的 [地址](https://segmentfault.com/a/1190000006178770#articleHeader4) 其实博客写的很好,只是 webpack更新了.所以还是要向官网看齐.

```shell
npm i -D webpack webpack-cli
npm i -D babel-loader babel-core
npm i -D babel-preset-env 
```

此时编辑我的js文件(用es6的语法). 然后 用webpack编译

```shell
npx webpack   //报错
```

错误如下: 

```
Module build failed (from ./node_modules/babel-loader/lib/index.js):
Error: Cannot find module '@babel/core'
 babel-loader@8 requires Babel 7.x (the package '@babel/core'). If you'd like to use Babel 6.x ('babel-core'), you should install 'babel-loader@7'.
```

好像是让我安装babel-loader@7, 那就安装吧:

```shell
npm i -D babel-loader@7
```

此时在编译 没问题了

主要代码:

```js
// .babelrc
{
  "presets": ["env"]
}
// package.json 中的 部分
 "devDependencies": {
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.5",
    "babel-preset-env": "^1.7.0",
    "webpack": "^4.23.0",
    "webpack-cli": "^3.1.2"
  }
// webpack.config.js中的部分
mode: 'development',  //此行不加 webpack会提示你要添加mode
module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: "babel-loader"
      }
    ]
  }
```

### 回合2

> 跟着官网来呗 [babel-loader](https://github.com/babel/babel-loader)

#### 安装有两个版本 都可用

- one

  ```
  // webpack 4.x | babel-loader 8.x | babel 7.x
  npm install -D babel-loader @babel/core @babel/preset-env webpack
  ```

 - two

   ```
   // webpack 4.x | babel-loader 7.x | babel 6.x
   npm install -D babel-loader@7 babel-core babel-preset-env webpack
   ```

**webpack.config.js配置**

```js
module: {
  rules: [
    {
      test: /\.m?js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['@babel/preset-env']
        }
      }
    }
  ]
}
```

一次成功. yes!~~  更多用法详见官网 [babel-loader](https://github.com/babel/babel-loader)


