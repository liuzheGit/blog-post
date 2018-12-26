---
title: 前端如何优雅的使用字体(font-family)
date: 2018-09-27 22:16:03
tags: [css,Font-family]
categories: Front-End
---


## 先看看大厂是如何做的 （截至2016.07）

1. 小米

``` css
font: 14px/1.5 "Helvetica Neue",Helvetica,Arial,"Microsoft Yahei","Hiragino Sans GB","Heiti SC","WenQuanYi Micro Hei",sans-serif;
```
小米公司优先使用Helvetica Neue这款字体以保证最新版本Mac用户的最佳体验，选择了Arial作为Win下默认英文字体及Mac的替代英文字体；中文字体方面首选了微软雅黑，然后选择了冬青黑体及黑体-简作为Mac上的替代方案；最后使用文泉驿微米黑兼顾了Linux系统。

2. 淘宝

``` css
font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;
```
代码中可以看出淘宝使用了Tahoma、Arial作为首选英文字体，中文字体首选了冬青黑体，由于Win下没有预装该款字体，所以显示出了后面的宋体（5b8b4f53为汉字宋体用 unicode 表示的写法，不用SimSun是因为 Firefox 的某些版本和 Opera 不支持 SimSun的写法）

3. 简书

```css
font-family: "lucida grande", "lucida sans unicode", lucida, helvetica, "Hiragino Sans GB", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
```
自认为简书的阅读体验很棒，我们看看简书所用的字体，简书优先选择了lucida家族的系列字体作为英文字体，该系列字体在Mac和Win上都是预装的，并且有着不俗的表现；中文字体方面将冬青黑体作为最优先使用的字体，同样考虑了Linux系统。



