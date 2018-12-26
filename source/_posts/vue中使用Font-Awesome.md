---
title: vue中使用Font Awesome
date: 2018-10-08 17:37:21
tags: [vue,FontAwesome]
categories: Front-End
---
# 在vue项目中使用Font Awesome

**Font Awesome**是一个十分优秀的第三方图标库，**Vue**是一个目前最火的前端框架，那么如何把二者结合起来，就是本文的目的。

## （一）官方

### 一、准备工作

**1. 安装基础依赖**

进入Vue项目文件夹，执行如下命令安装基础依赖库：

```sh
npm i --save @fortawesome/fontawesome-svg-core
npm i --save @fortawesome/vue-fontawesome			
```

**2. 安装样式依赖**

Font Awesome 为我们提供了`Solid`,`Regular`, `Brands`这三种免费样式，执行如下命令安装：

```sh
npm i --save @fortawesome/free-solid-svg-icons
npm i --save @fortawesome/free-regular-svg-icons
npm i --save @fortawesome/free-brands-svg-icons
```



**3. 配置vue项目下的`src/main.js`**

配置如下：

```javascript
import { library } from '@fortawesome/fontawesome-svg-core'
import { fas } from '@fortawesome/free-solid-svg-icons'
import { far } from '@fortawesome/free-regular-svg-icons'
import { fab } from '@fortawesome/free-brands-svg-icons'
import { FontAwesomeIcon, FontAwesomeLayers, FontAwesomeLayersText }
 from '@fortawesome/vue-fontawesome'
 
library.add(fas, far, fab) //添加3中样式
 
Vue.component('font-awesome-icon', FontAwesomeIcon)  // 我只用这个
Vue.component('font-awesome-layers', FontAwesomeLayers)
Vue.component('font-awesome-layers-text', FontAwesomeLayersText)
```



### 二、样式介绍

三种免费样式，使用的时候分别对应不同的前缀

* `solid`样式，前缀为`fas` 
* `regular`样式，前缀为`far`
* `brands`样式，前缀为`fab`  



### 三、基本用法 显示图标

1. 显示

   a. 我们使用 font-awesome-icon 标签来显示图标，icon 属性中可以设置样式前缀、以及图标名字。

   ```html
   <font-awesome-icon :icon="['fas', 'square']" />
   <font-awesome-icon :icon="['far', 'square']" />
   <font-awesome-icon :icon="['fab', 'accessible-icon']" />
   ```



   b. 如果是 solid 样式（前缀为：fas），则前缀可以省略。比如上面第一个图标等效下面写法：

   ```html
   <font-awesome-icon icon="square" />
   ```

2. 设置图标大小

   默认情况下图标和当前文字的大小是一样的。我们可以通过 size 属性在此基础上作调整，该属性支持多种类型的设置方式

   ```html
   <font-awesome-icon icon="chess-knight"  />
   <font-awesome-icon icon="chess-knight" size="xs" />
   <font-awesome-icon icon="chess-knight" size="lg"  />
   <font-awesome-icon icon="chess-knight" size="2x" />
   ```

3. 固定图标宽度
  使用 fixed-width 可以固定图标宽度。

   ```html
   <font-awesome-icon icon="home" fixed-width /> home <br>
   <font-awesome-icon icon="child" fixed-width /> help <br>
   <font-awesome-icon icon="cog" fixed-width /> settings <br>
   ```

4. 旋转图标
```html
    <font-awesome-icon icon="chess-knight" rotation="0" />
    <font-awesome-icon icon="chess-knight" rotation="90" />
    <font-awesome-icon icon="chess-knight" rotation="180" />
    <font-awesome-icon icon="chess-knight" rotation="270" />
```

5. 翻转图标
```html
	<font-awesome-icon icon="chess-knight"  />
    <font-awesome-icon icon="chess-knight" flip="horizontal" />
    <font-awesome-icon icon="chess-knight" flip="vertical" />
    <font-awesome-icon icon="chess-knight" flip="both" />
```

6. 旋转动画效果
	a. 添加 spin 属性可以让图标不停地顺时针旋转。
```html
	<font-awesome-icon icon="arrow-circle-down" spin />
```
	b.添加 pulse 属性同样可以让图标旋转，但它不像 spin 那样是均匀地变化角度，而是 0 度、45 度、90 度...这样跳跃地变化。
```html
	<font-awesome-icon icon="arrow-circle-down" pulse />
```

7. 图片居左、居右显示
有时我们需要让图标一直在最左侧或最右侧（在做文字围绕图标效果时会用到）。
```html
<font-awesome-icon icon="clipboard-list" size="2x" pull="left"/>
Font Awsome is awsome. Font Awsome is awsome. Font Awsome is awsome.
```
8. 给图标加上边框(border)
```html
<font-awesome-icon icon="clipboard-list" size="2x" pull="right" border />
```

### 四、进阶用法
**a. 变形、自由变换（Transforms）**
​	1. 变形、自由变换（Transforms）
```html
<font-awesome-icon icon="clipboard-list" />
<br>
<font-awesome-icon icon="clipboard-list" transform="shrink-6 left-4" />
```
	2. 下面样例将第二个图标顺时针旋转 42 度：
```html
<font-awesome-icon icon="clipboard-list" />
<br>
<font-awesome-icon icon="clipboard-list" :transform="{ rotate: 42 }" />
```

**b. 遮罩**
```html
<font-awesome-icon icon="star" />
<font-awesome-icon  icon="star" mask="circle"  />
<font-awesome-icon  icon="star" mask="square"  />
```
**c. 多个图标的组合使用**
```html
<font-awesome-layers class="fa-lg">
  <font-awesome-icon icon="circle" style="color: green;"/>
  <font-awesome-icon icon="check" transform="shrink-6" style="color: white;" />
</font-awesome-layers>
```

**d. 图标与文字的组合使用**
```html
<font-awesome-layers full-width class="fa-4x">
  <font-awesome-icon icon="star"/>
  <font-awesome-layers-text transform="down-1 right-1 shrink-14" value="hello" style="color:white" />
</font-awesome-layers>
```

**e.动态改变图标（图标的绑定）**
```html
<template>
  <font-awesome-icon :icon="icon" />
</template>
 
<script>
export default {
  computed: {
    icon() {
      return ['fas', 'coffee']
    }
  }
}
</script>
```


## （二）Vue-Awesome 内置Font Awesome图标

> 基于 Vue.js 的强大 SVG 图标组件。已内置 Font Awesome 图标。
Vue-Awesome 是基于 [Vue.js](https://vuejs.org/) 的 SVG 图标组件，内置图标来自 [Font Awesome](https://fontawesome.com/)。

查看[此处](https://justineo.github.io/vue-awesome/demo/)的 demo 一睹为快。

### 安装

```sh
npm install vue-awesome
```

### 使用方法

```html
<!-- 基础用法 -->
<v-icon name="beer"/>

<!-- 添加选项 -->
<v-icon name="sync" scale="2" spin/>
<v-icon name="comment" flip="horizontal"/>
<v-icon name="code-branch" label="Forked Repository"/>

<!-- 堆叠图标 -->
<v-icon label="No Photos">
  <v-icon name="camera"/>
  <v-icon name="ban" scale="2" class="alert"/>
</v-icon>
```

Font Awesome 5 开始把所有图标分成了多个包。Vue-Awesome 的图标都来自其中的免费图标，而免费图标分别来自 3 个不同的图标包：`regular`、`solid` 和 `brands`。因为 `solid` 下的免费图标数量最多，所以我们选择按如下方式来组织图标：

- 所有来自 `solid` 包的图标位于 `vue-awesome/icons` 目录下，且 `name` prop 的值不带前缀。
- 来自 `regular` 和 `brands` 的图标位于 `vue-awesome/icons/regular` 和 `vue-awesome/icons/brands` 目录下，且 `name` prop 的值需要添加前缀，例如 `regular/flag` 或者 `brands/reddit`。

请访问 [Font Awesome 官网](https://fontawesome.com/)以查询可以使用的 `name` 值，如 `beer`、`file`、`camera` 等。



### 引入

**用 npm 与 vue-loader 基于 ES Module 引入（推荐用法）**


```js
import Vue from 'vue'  // 必须

/* 在下面两种方式中任选一种 */

// 仅引入用到的图标以减小打包体积
import 'vue-awesome/icons/flag'

// 或者在不关心打包体积时一次引入全部图标
import 'vue-awesome/icons'

/* 任选一种注册组件的方式 */

import Icon from 'vue-awesome/components/Icon' // 必须



// 全局注册（在 `main .js` 文件中）
Vue.component('v-icon', Icon)

// 或局部注册（在组件文件中）
export default {
  components: {
    'v-icon': Icon
  }
}
```



## 参考

http://www.hangge.com/blog/cache/detail_2104.html

https://fontawesome.com/

https://www.npmjs.com/package/@fortawesome/vue-fontawesome

https://github.com/Justineo/vue-awesome/blob/master/README.zh_CN.md
