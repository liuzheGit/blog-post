---
title: css深入浅出
date: 2018-09-26 18:07:40
tags: css
categories: Front-End
---
## CSS 深入浅出

1. 永远不要定父级的高度。用padding撑
2. outline 是不占位的。


### CSS的宽度和高度
**文档流（Normal Flow） 普通流 常规流**
    内联元素的宽高
    块级元素的宽高
    水平居中
    垂直居中
    文字溢出省略（多行）
**盒模型**
    一比一的 div
    outline
    border 调试大法
### 总结 
1. 如果div中只有内联元素。那么它的高度是内联元素的行高。（字体默认行高 是字体设计者确定的）
2. &nbsp； --no break space; 不换行的空格
3. text-align: justify ? 在多行中 行首和行尾对齐
4. html解析代码时会把内联元素之内的显示 之外的不显示
5. inline元素之间用空格或回车 则他们之间会显示间隙
6. css的调试是加border
7. word-break: break-all; 只要到行尾就断开
8. div的宽度不是由文字决定的
9. margin能不能使父元素变高取决于margin有没有被东西包着(如： border、padding、overflow：hidden)
10. margin合并
11. overflow：hidden； 不到万不得已，不要用；

div的高度是由它内部的文档流中元素的总和决定的。 
**文档流**：其实是叫普通流（normal-flow）元素按照其在HTML中的位置顺序决定排布过程。
内联元素从左到右 ，块级元素从上到下,只要不是float和绝对定位的，都在普通流中。

脱离文档流：就是计算高度不叫我。
相对定位： 计算高度计算他。
内联元素的margin和padding会影响父级的宽度，但不会影响高度。
1个1：1的div用 ： padding-top: 100%;




中文字的对齐：
![](media/15378384261294/15378408191332.jpg)

清楚浮动
![](media/15378384261294/15378410630358.jpg)

    ### 堆叠上下文
    学会 调试（实验） text-indent/ margin: -5px;
    ![](media/15378384261294/15378500552333.jpg)

### icon
sprites 精灵图
1. 把ps中的单个图层导出为PNG。
2. 如果是PNG，扣图是用选择工具选中然后右键copy；
3. html 实体编号entity；

### 移动端

用 @media，一个条件是一个括号
```css
@media (max-width: 320px) { /* 0-320px */
    ...
}

@media (min-width: 321px) and (max-width: 375px) { /*321px - 275px*/
    ...
}
```

@media 可以作用到css文件上 如： `<link rel="stylesheet" media="only screen and (max-width:320px)">`

mobile first 移动优先

classList.toggle('active') 原生的toggle class

980px 是业界 移动端模拟pc的大小。

### 移动端滑动
[jquery模拟的](https://github.com/mattbryson/TouchSwipe-Jquery-Plugin)，vue 也有对应的。
移动端是没有滚动条的，他有的是位置指示器。

### flex布局
flex-direction: 可以确定主轴的方向


### 布局套路
**用作布局的div只用来用作布局，不要加内容等，给宽高给到最里面让他去撑**

1. 兼容ie8 用Float布局 定宽
2. 用Flex布局

注意： 不写死width和height、尽量用高级语法： calc、flex 、如果是ie8 则写死

布局1： Float： 儿子用float 父级加clear: both; 
``` css
.clearfix::after{
  content: '';
  display: block;
  clear: both;
} /* 兼容ie8 */

.clearfix{
  zoom: 1;
}  /* 可以兼容ie6 */
```

布局2：  给父级加`display: flex`
给一个没有宽度的div加一个 margin的 负值，那么它会被撑开。 如果最后这里在做移动端的时候出现滚动条则用 `overflow: hidden` 去除。
### 负margin 用一个xxx包着做。

### 用shift tab实现 负缩进 


### 不用img标签 解决img变形

### 用padding去和兄弟元素的高度对齐。

## 动态REM  - 手机专用

宽度单位： 
1. px：像素 
2. em：一个M(它的宽高一致所有说是一个M)的宽度（一个汉字的宽度）
3. rem: root em 根元素的font-size的大小
4. vh/vw: viewport height

**12px法则**
网页的默认font-size:16px;
chrome可以设置最小是12px 小于12px的 显示还是12px

1. 百分比布局
2. 整比例缩放

**一切单位以宽度 ， 就能保证完美还原设计**

**如何引入rem的使用呢？**
1rem = html font-size = page width;

切记html的font-size 不要太小，可以和其他单位混用。




