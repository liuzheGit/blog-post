---
title: clip-path
date: 2018-10-16 15:52:37
tags: css
categories: Front-End
---

# clip-path

clip-path属性可以创建一个只有元素的部分区域可以显示的剪切区域。区域内的部分显示，区域外的隐藏。剪切区域是被引用内嵌的URL定义的路径或者外部svg的路径，或者作为一个形状例如[circle()](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/circle).。clip-path属性代替了现在已经弃用的剪切 [clip](https://developer.mozilla.org/en-US/docs/Web/CSS/clip)属性。



## 实例

```css
img{
  display: block;
  width: 155px;
  height: 160px;
  border: 1px solid #f7f7f9;
  border-radius: 6px;
  clip-path:polygon(50% 0,100% 50%,50% 100%,0 50%);
  transition: clip-path 1s ;
}

img:hover{
  clip-path:polygon(0 0,100% 0,100% 100%,0 100%);
}
```

![hoverDemo](/images/clip-pathDemo.GIF)


