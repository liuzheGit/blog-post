---
title: css技巧-color的巧用
date: 2018-11-26 11:05:11
tags: css
categories: Front-End
---
## 引言
这个技巧来自 张鑫旭的css世界的讲解.

## 延伸
具体是: css中 有很多的属性中的颜色值默认的 是`color`的值, 如: border-color/outline/box-shadow和text-shadow等.

## 实例
实际开发的例子: 上传图片的时候,会做美化比如这样:
![css图片上传](/images/css上传.png)
hover的时候可以整体变个色.
这种方方正正、简简单单的图形最适合使用三三两两的CSS代码绘制了。通常， 我们使用width/height外加一个background-color绘制加号的, 核心CSS代码如下: 

```css
.add {
    border: 2px dashed #ccc;
}

.add:before, .add:after {
    background: #ccc;
}

/* hover的时候 变个色*/
.add:hover {
    background: #06C;
}

.add:hover:before, .add:hover:after {
    background: #06C;
}
```

功能上没有问题, 可是当我们`hover`变色的时候, 需要同时重置3处(元素本身以及两个伪元素)颜色. 实际上, 如果这里不适用`background-color`, 而是使用`border`来绘制加号, 则代码会简单很多, 如下: 
```css
.add {
    color: #ccc;
    border: 2px dashed;
}
.add:before {
    border-top: 10px solid;
}
.add:after {
    border-left: 10px solid;
}
/* hover的时候 变个色*/
.add:hover {
    color: #06C;
}
```

可以看到, 使用`border`实现, 我们hover变色的时候, 只需要重置1处, 也就是重置元素本身的`color`就可以了, 因为整个图形都是使用border绘制的, 同时颜色缺省, 所以所有图形颜色自动跟着一起变化了.
演示效果 [张鑫旭](https://demo.cssworld.cn/4/4-1.php)
[我的演示](http://js.jirengu.com/sobol/3/edit)




