---
title: flexBox
date: 2018-07-08 15:28:46
tags: [css, flex]
categories: Front-End
---
###flexBox 弹性盒子 by [$css-stricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

------

#### 1.flex的兼用性

lex布局是不支持ie8，9的，所以建议，如果要做兼容ie8的pc端项目，还是老老实实用浮动布局吧~！但是现在是H5的时代，移动端我们还是放心大胆用吧，请抛弃恶心的清除浮动！

#### 2.语法速记

 作用的对象：

> container父级 说明：(d) 表示 默认

- 添加flex属性：
  `display: flex/line-flex;`
- 确定主轴方向：
  `flex-direction: row(d) | row-reverse | column | column-reverse`
- 换行方式：
  `flex-wrap: nowrap(d) | wrap | wrap-reverse`
- 主轴和换行结合:
  `flex-flow: <'flex-direction'> || <'flex-wrap'>`。默认是 `flex-flow: row nowrap`
- 沿主轴的对齐方式：
  `justify-content: flex-start(d) | flex-end |center | space-between | space-around | space-evenly`
- 沿主轴项目的横向放置行为：
  `align-items: flex-start | flex-end | center | stretch(d) | baseline`
- 当主轴横向有空余空间是，类似于横向的`justify-content`:对于只有一行的不起作用
  `align-content: flex-start | flex-end | center | stretch(d) | space-between | space-around`

> item 子级 -------- 请注意float，clear并且vertical-align对Flex项目没有影响

- order属性：（0是默认）order从小到大排列
  `order: <integer>`
- flex-grow属性：(0是默认,负数无效)item的必要的增长能力，如果一个设为2，其余的设为1，则设置为2的占据的大小是1的2倍。
  `flex-grow: <number>`
- flex-shrinks属性：(1是默认,负数无效) 和 flex-grow相反。是一种收缩能力
  `flex-shrinks:<number>`
- 分配剩余空间之前定义元素的默认大小:如果设置为0，则不会考虑内容的额外空间。如果设置为auto，多余空间将根据其flex-grow值分配
  `flex-basis: <length> | auto(d)`
- flex属性：是flex-grow | flex-shrinks | flex-basis 的结合.第二个和第三个属性时可选的。默认是：`0 1 auto`
  `flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]`
- align-self属性：可以用单独的属性。覆盖默认对齐方式
  `align-self: align-self: auto | flex-start | flex-end | center | baseline | stretch;`



#### 3.详解

by -- [CSND](https://blog.csdn.net/lc941015/article/details/79098933)

```css
.box{
    /* flex布局第一步：找到你要布局元素的父元素 */
    display:flex;
    /* 第二步：判断方向：元素是横着排还是竖着排，默认为横着排，当项目空间不够时，是否换行 */
    flex-direction: row（横向） | column（纵向）;
    flex-wrap:nowrap(默认不换行) | wrap （换行，新元素在下面一行） | wrap-reverse（换行，新元素在上面一行）
    /* 第三步：根据方向，进行布局操作,注意敲黑板啦
        当为横向时，水平布局的操作用justify-content属性，垂直方向的操作用align-items属性；
        当为纵向时，两属性的作用正好相反，水平布局的操作用align-items属性，垂直方向的操作用justify-content属性；
        以上两个属性是用的最多的属性了。
    */
    justify-content: flex-start | flex-end | center | space-between | space-around;
    align-items: flex-start | flex-end | center | baseline | stretch;
}
```

#### justify-content 和 align-items 属性（设置到父元素）

- justify-content: flex-start 相当于左浮动
- justify-content: flex-end 相当于右浮动，具体不赘述，同上
- justify-content: center 让某个元素水平居中
- justify-content: space-between 这个就非常好用的 ，两个子元素情况下，一个元素左对齐，一个元素右对齐。三个元素情况下就无敌了，能实现一个元素居中，一个元素左对齐，一个元素右对齐。放以前，中间居中的都不知道有多麻烦。
- justify-content: space-around 每个子元素两侧的间距都相等，且为项目到边框距离的两倍。
- align-items: flex-start 垂直方向的 上对齐。
- align-items: flex-end 垂直方向的 下对齐。
- align-items：center 最好用的竖直居中
- align-items：stretch 如果元素没设置高的话，高度将与父元素相等（铺满整个元素）
- align-items：baseline 与元素第一行文字的头对齐，我暂时没找到用此属性的地方

#### 设置到子元素的常用属性：

- order: 设置排序的，数值越小，元素越靠前（用的不多）
- flex-grow: 设置项目的放大比例 有点栅格化布局的意思 比如三个子元素，全部设置 flex-grow: 1 则在父元素内 宽度都相等 （3等分）
- flex-shrink：设置项目的缩小比例，当空间不足时，所有项目会默认等比例缩小。当设置flex-shrink:0 时，当空间不足时元素也不会缩小
- 注意 ：若设置了元素的宽度,还有设置 flex-shrink:0 ，否则项目空间不足时，元素会缩小，设置的宽度就不生效了
- flex-basis：百分比或者像素，当项目空间充足时，给子元素设置一个默认的宽度，默认auto（项目的本来大小）
- align-self：这个属性呢，就是单元素版的align-items（设置后，所有子元素都会生效），但如果只想让一个元素居中，就设置改元素align-self：center

#### 4.flex布局常用demo

1.带有icon的标题,icon居中

```css
.title{
      margin-top:20px;
      display: flex;
      width: 100%;
      justify-content: center;
      align-items: center;
    }
```

2.左中右布局，左边右定宽，中间部分自适应。

```css
    在父元素中设置 justify-content: space-between;在左右子元素中设置flex-shrink:0(防止空间不足时缩小);在中间元素下设置flex-grow:1(让它撑满中间区域);
```

3.input输入框跟不定长的label撑满一行

```css
其实跟上面要使用的方法差不多，将父元素设置justify-content: space-between，将要固定的元素(label)设置flex-shrink:0，将要铺满的元素(input)设置flex-grow:1。
```

4.流式布局（一排放4个，放不下就换行）

```css
  .flow{
      display: flex;
      flex-wrap:wrap;
      justify-content: flex-start;
      border:1px solid #e3e3e3;
    }
    .flow .item{
      flex:0 0 22%;
      /*
        等同于
        flex-grow: 0;
        flex-shrink:0 ;
        flex-basis:22%;
      */
      padding-bottom: 22%;/* 做到宽高相等 */
      margin: 1.5%;
      background: yellow;
    }
```

