---
title: Font Awesome使用
date: 2018-10-08 16:30:54
tags: [icon, FontAwesome]
categories: Front-End
---

# Font Awesome字体图标

## 一，什么是字体图标

（1）现在比较流行使用字体图标，所谓字体图标其实就是一个包含许多图标的字体库。同我们常用的字体一样，这个也可以理解为一种特殊字体，只不过里面包含的都是图标。

（2）既然是字体，那么最方便的就是可以随意在代码中更改颜色和大小而不会失真。这样不需要因为要适配各种尺寸而制作多个图片，或者做多套颜色的图标用来标识不同状态。

（3）无论是按钮图标还是导航栏图标，也不管是网站开发还是移动应用开发，字体图标都能适用。

## 二，Font Awesome 图标字体库

Font Awesome

 是一套目前最受欢迎最全面的图标字体库。这套图标字体集几乎囊括了网页中可能用到的所有图标和社交网络图标、Web 应用程序图标和编辑器图标等等。



网站地址：[官网地址](http://fontawesome.io/)  [GitHub地址](https://github.com/FortAwesome/Font-Awesome)



主要特色如下：

✓ 一种字体，包含1341个免费图标（截至5.3.1版本）；

✓ 纯 CSS 控制，能够轻松定义图标的颜色、大小、阴影以及任何 CSS 能够实现的效果；

✓ 无限缩放，svg矢量图标在任何尺寸下都一模一样；

✓ 免费使用，包括商业和非商业项目；

✓ 支持 Internet Explorer 7 浏览器；

✓ 简单，易用；

[点击此处查看全部](http://fontawesome.io/icons/)

## 三，Font Awesome的配置

（1）首先将整个字体库文件夹`font-awesome`放到工程项目中。 

（2）在html页面的头部把 `font-awesome.min.css `引进来。

```html
<link rel="stylesheet" href="font-awesome/css/font-awesome.min.css">
```

## 四，Font Awesome的使用样例

在页面中的任何地方都可以使用 

<i>

 标签来使用Font Awesome字体图标。



**1，最简单的样例**

通过在class中使用

 

fa 

前缀以及图标名字，可以显示出相应的图标（内联样式）

```html
<i class="fa fa-camera-retro"></i> fa-camera-retro
```



**2，相对于内容大小，放大图标尺寸**

使用

fa-lg, fa-2x, fa-3x, fa-4x, fa-5x

样式可以让图标相对于内容，尺寸增大33%，变成2倍，3倍，4倍，5倍。

（注意：如果发现图标上下有被隐藏的情况，你可以通过适当增加line-height 来解决）



**3，固定宽度图标**
使用 fa-fw 可以固定图标宽度



**4，列表图标**
使用 fa-ul 和 fa-li 可以很方便地替换list列表默认图标



**5，有边框且漂浮的图标**
使用 fa-border 与 fa-pull-right 或者 fa-pull-left 组合使用，可以很方便地实现引用或文章图标。



**6，图标旋转动画** 

使用 fa-spin 可以让图标匀速旋转，使用 fa-pulse 可以让图标只按8个角度旋转。



**7，旋转、翻转图标**
使用 fa-rotate-* 和 fa-flip-* 可以分别实现图标的旋转和翻转。



**8，叠加图标**
要叠加多个图标，使用 fa-stack 设置容器。fa-stack-1x 表示正常大小的图标，fa-stack-2x 表示更大的图标。 fa-inverse 可以让图标反色。
