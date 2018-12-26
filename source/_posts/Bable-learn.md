---
title: Bable_learn
date: 2018-09-08 15:28:09
tags: [JavaScript, es6]
categories: Front-End
---
# Babel

目的是为了 用es6的特性,所以用到Babel

## 安装 babel-cli ` 不推荐全局安装`

 `npm install --save-dev/-D babel-cli`

> 注: 本地安装如果想用babel 需要到`./node_modules/.bin/babel`才可以使用，所以可以用npm的npx执行`npx babel`这里前缀加上npx可以自动去找.bin目录下的babel可执行文件. 如果没有就向上寻找如果全局也没有就会提示没有安装babel.

## 接着上一步 需要在项目跟目录创建 `.babelrc`文件

> 推荐配置

```json
{
  "presets": [
    "es2015",
    "stage-0",
    //"env"  //env不仅可以转换es6，还可以转换es7\es8代码到es5
  ],
  "plugins": ["transform-runtime"]
}

```

## babel-cli的用法

- 直接输出到控制台

  ```
  npx babel script.js
  ```

- 单文件编译到单文件 用 `--out-file / -o`

  ```
  npx babel script.js -o script-compiled.js
  ```

- 监听同时编译单文件 `--watch / -w`

  ```
  npx babel script.js -w -o script-compiled.js
  ```

- 编译目录 `--out-dir / -d` 这不会覆盖其他文件或目录

  ```
  npx babel src -d dist
  ```

- 编译目录到一个单文件中

  ```
  npx babel src -d script-compiled.js
  ```

- 忽略文件 `--ignore`

> 如忽略spec和test文件
>
> ```
> npx babel src -d lib --ignore spec.js,test.js
> ```

- 复制文件

> 复制不需要编译的文件
>
> ```
> npx babel src --out-dir lib --copy-files
> ```

- 传输文件

> 通过标准输入传入一个文件并输出到 `script-compiled.js`
>
> ```
> npx babel --out-file script-compiled.js < script.js
> ```

- 使用插件

> 使用 `--plugins` 选项来指定编译中要使用的插件
>
> ```
> npx babel script.js --out-file script-compiled.js --plugins=transform-runtime,transform-es2015-modules-amd
> ```

- 使用 Presets

> 使用 `--presets` 选项指定编译中要使用的插件
>
> ```
> npx babel script.js --out-file script-compiled.js --presets=es2015,react
> ```

- 忽略 .babelrc 文件

> 忽略项目中 `.babelrc` 文件的配置并使用 cli 选项，例如，为一个自定义的构建
>
> ```
> npx babel --no-babelrc script.js --out-file script-compiled.js --presets=es2015,react
> ```