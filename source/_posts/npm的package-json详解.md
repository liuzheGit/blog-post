---
title: npm的package.json详解
date: 2018-11-10 17:44:55
tags: ['JavaScript', 'npm']
categories: Front-End
---

## npm中package.json详解

> 参见 [https://blog.csdn.net/naipeng/article/details/53178062](https://blog.csdn.net/naipeng/article/details/53178062)

通常我们使用npm init命令来创建一个npm程序时，会自动生成一个`package.json`文件。`package.json`文件会描述这个NPM包的所有相关信息，包括作者、简介、包依赖、构建等信息，格式是严格的JSON格式。

 

**常用命令**

npm i --save packageName   安装依赖包

npm i --save-dev packageName

npm i webpack@1.2.1   安装指定版本的包，版本号用@符号连接

 

**属性介绍**

**name**

`name`和`version`是package.json中最重要的两个字段，也是发布到NPM平台上的唯一标识，如果没有正确设置这两个字段，包就不能发布和被下载。

**version**

包的版本号。如"1.0.0"。

**description**

包的描述信息，将会在`npm search`的返回结果中显示，以帮助用户选择合适的包。

**keywords**

包的关键词信息，是一个字符串数组，同上也将显示在`npm search`的结果中。

**homepage**

包的主页地址。

**bugs**

包的bug跟踪主页地址。

**license**

包的开源协议名称。

**author**

包的作者。

**contributors, maintainers**

包的贡献者，是一个数组。

**files**(较少用)

包所包含的所有文件，可以取值为文件夹。通常我们还是用`.npmignore`来去除不想包含到包里的文件。

**main**

包的入口文件。

**bin**(较少用)

如果你的包里包含可执行文件，通过设置这个字段可以将它们包含到系统的`PATH`中，这样直接就可以运行，很方便。

**man**(较少用)

为系统的`man`命令提供帮助文档。帮助文件的文件名必须以`数字`结尾，如果是压缩的，需要以`.gz`结尾。

```
"man": ["./man/foo.1", "./man/bar.1", "./man/foo.2" ]
```

**directories**(较少用)

CommonJS包所要求的目录结构信息，展示项目的目录结构信息。字段可以是：lib, bin, man, doc, example。值都是字符串。

**repository**

包的仓库地址。

```
"repository": {
    "type": "git",
    "url": "git+https://github.com/rainnaZR/es6-react.git"
  },
```

**scripts**

通过设置这个可以使NPM调用一些命令脚本，封装一些功能。

```
"scripts": {"start": "babel-node src/pages/index.js",
    "build": "webpack --config config/webpack.config.js",
    "watch": "webpack-dev-server --config config/webpack.config.js --hot --inline --progress"
  }
```

**config**

添加一些设置，可以供`scripts`读取用，同时这里的值也会被添加到系统的环境变量中。

```
"config": {
  "port": "8080"
}
```

`npm start`的时候会读取到`npm_package_config_port`环境变量。

**dependencies**

指定依赖的其它包，这些依赖是指包发布后正常执行时所需要的，也就是线上需要的包。使用下面的命令来安装：

```
npm install --save packageName
```

如果是开发中依赖的包，可以在`devDependencies`设置。

**devDependencies**

这些依赖只有在开发时候才需要。使用下面的命令来安装：

```
npm install --save-dev packageName 
```

**peerDependencies**

相关的依赖，如果你的包是插件，而用户在使用你的包时候，通常也会需要这些依赖（插件），那么可以将依赖列到这里。

如`karma`, 它的`package.json`中有设置，依赖下面这些插件：

```
"peerDependencies": {
  "karma-jasmine": "~0.1.0",
  "karma-requirejs": "~0.2.0",
  "karma-coffee-preprocessor": "~0.1.0",
  "karma-html2js-preprocessor": "~0.1.0",
  "karma-chrome-launcher": "~0.1.0",
  "karma-firefox-launcher": "~0.1.0",
  "karma-phantomjs-launcher": "~0.1.0",
  "karma-script-launcher": "~0.1.0"
}
```

**bundledDependencies**

绑定的依赖包，发布的时候这些绑定包也会被一同发布。

**optionalDependencies**（较少用）

即使这些依赖没有，也可以正常安装使用。

**engines**（较少用）

指定包运行的环境。

```
"engines": {
  "node": ">=0.10.3 < 0.12",
  "npm": "~1.0.20"
}
```

**os**（较少用）

指定你的包可以在哪些系统平台下运行。

```
"os": [ "darwin", "linux", "!win32" ]
```

**cpu**（较少用）

可以指定包运行的cpu架构。

**private**

设为`true`这个包将不会发布到NPM平台下。

**publishConfig**（较少用）

这个字段用于设置发布时候的一些设定。尤其方便你希望发布前设定指定的`tag`或`registry`。

 

如下：

```
{
  "name": "react",
  "version": "1.0.0",
  "description": "Command line instructions",
  "keywords": [
    "react",
    "es6",
    "react with es6"
  ],
  "homepage": "https://github.com/rainnaZR/es6-react",
  "bugs": {
    "url": "https://github.com/rainnaZR/es6-react",
    "email": "111@163.com"
  },
  "license": "ISC",
  "author": "ZRainna",
  "main": "src/pages/index.js",
  "directories": {
    "tests": "tests",
    "lib":"lib",
    "docs":"docs"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/rainnaZR/es6-react.git"
  },
  "scripts": {"start": "babel-node src/pages/index.js",
    "build": "webpack --config config/webpack.config.js",
    "watch": "webpack-dev-server --config config/webpack.config.js --hot --inline --progress"
  },
  "babel": {
    "presets": [
      "es2015-node5"
    ]
  },
  "devDependencies": {
    "webpack": "^1.13.2",
    "webpack-dev-server": "^1.16.1"
  },
  "dependencies": {
    "babel-loader": "^6.2.5",
    "babel-preset-es2015": "^6.14.0",
    "babel-preset-react": "^6.11.1",
    "react": "^15.3.2",
    "react-dom": "^15.3.2",
    "react-redux": "^4.4.5",
    "react-router": "^2.8.1",
    "redux": "^3.6.0"
  }
}
```