---
title: scss快速入门
date: 2018-10-22 17:05:30
tags: [css, scss]
categories: Front-End
---

## 1.引入变量

### 变量声名

`$hightlight-color: #F90;`

代码块中的变量可以和外部的重名, 互不影响.

### 变量引用

凡是`css`属性的标准值（比如说1px或者bold）可存在的地方，变量就可以使用。

### 中划线还是下划线

可以互相使用, 就是 声名用`-`时,引用可以`_`,不过还是推荐一致更好.

#2.父选择器标识符`&`

```css
article a {
  color: blue;
  &:hover { color: red }
}
```

编译后

```css
article a { color: blue }
article a:hover { color: red }
```

>  `&`符号前边可以再加选择器

### 属性也可以嵌套

```scss
nav {
  border: {
    color: red;
    style: solid;
    width: 5px;
  }
}
```

## 3.导入css/sass文件

### 默认变量值用 `!default`



## 4.  静默注释

```scss
body {
  color: #333; // 这种注释内容不会出现在生成的css文件中
  padding: 0; /* 这种注释内容会出现在生成的css文件中 */
}
```

## 5.混合器 `@mixin`

`sass`的混合器`@mixin`实现大段样式的重用.

用 @mixin 声名. 用 @include 使用.

```scss
@mixin rounded-corners {
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}

notice {
  background-color: green;
  border: 2px solid #00aa00;
  @include rounded-corners;
}
// sacc 最终生成

.notice {
  background-color: green;
  border: 2px solid #00aa00;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
```



### 何时使用混合器

利用混合器，可以很容易地在样式表的不同地方共享样式。如果你发现自己在不停地重复一段样式，那就应该把这段样式构造成优良的混合器，尤其是这段样式本身就是一个逻辑单元，比如说是一组放在一起有意义的属性。

判断一组属性是否应该组合成一个混合器，一条经验法则就是你能否为这个混合器想出一个好的名字。如果你能找到一个很好的短名字来描述这些属性修饰的样式，比如`rounded-corners``fancy-font`或者`no-bullets`，那么往往能够构造一个合适的混合器。如果你找不到，这时候构造一个混合器可能并不合适。

### 混合器中的CSS规则

混合器中不仅可以包含属性，也可以包含`css`规则，包含选择器和选择器中的属性，如下代码:

```scss
@mixin no-bullets {
  list-style: none;
  li {
    list-style-image: none;
    list-style-type: none;
    margin-left: 0px;
  }
}
```

### 给混合器传参

 例子

```scss
// 定义
@mixin link-colors($normal, $hover, $visited) {
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}

// 使用
a {
  @include link-colors(blue, red, green);
}

//Sass最终生成的是：

a { color: blue; }
a:hover { color: red; }
a:visited { color: green; }
```

当你@include混合器时，有时候可能会很难区分每个参数是什么意思，参数之间是一个什么样的顺序。为了解决这个问题，`sass`允许通过语法`$name: value`的形式指定每个参数的值。这种形式的传参，参数顺序就不必再在乎了，只需要保证没有漏掉参数即可：

```scss
a {
    @include link-colors(
      $normal: blue,
      $visited: green,
      $hover: red
  );
}
```

### 默认参数值

为了在`@include`混合器时不必传入所有的参数，我们可以给参数指定一个默认值。参数默认值使用`$name: default-value`的声明形式，默认值可以是任何有效的`css`属性值，甚至是其他参数的引用，如下代码：

```scss
@mixin link-colors(
    $normal,
    $hover: $normal,
    $visited: $normal
  )
{
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
```

如果像下边这样调用：`@include link-colors(red)` `$hover`和`$visited`也会被自动赋值为`red`。



## 6.使用选择器继承来精简CSS

继承一个类的所有样式到被继承的地方:

```scss
//通过选择器继承继承样式
.error {
  border: 1px solid red;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}

// 渲染后
.error, .seriousError {
  border: 1px solid red;
  background-color: #fdd;
}

.seriousError {
  border-width: 3px;
}
```

通常使用继承会让你的`css`美观、整洁。因为继承只会在生成`css`时复制选择器，而不会复制大段的`css`属性。但是如果你不小心，可能会让生成的`css`中包含大量的选择器复制,解决办法是:

不要在`css`规则中使用后代选择器去继承`css`规则.如:

```scss
.foo .bar { @extend .baz; }
.bip .baz { a: b; }
```

在上边的例子中，`sass`必须保证应用到.baz的样式同时也要应用到`.foo .bar`（位于class="foo"的元素内的class="bar"的元素）。例子中有一条应用到`.bip .baz`（位于class="bip"的元素内的class="baz"的元素）的`css`规则。当这条规则应用到`.foo .bar`时，可能存在三种情况，如下代码:

```scss
<!-- 继承可能迅速变复杂 -->
<!-- Case 1 -->
<div class="foo">
  <div class="bip">
    <div class="bar">...</div>
  </div>
</div>
<!-- Case 2 -->
<div class="bip">
  <div class="foo">
    <div class="bar">...</div>
  </div>
</div>
<!-- Case 3 -->
<div class="foo bip">
  <div class="bar">...</div>
</div>
```

> 不要用后代选择器去继承。

## 总结

变量是`sass`提供的最基本的工具. 通过变量可以让独立的`css`值变得可重用, 无论是在一条单独的样式还是一段样式. 变量和混合器的命名可以通用`-`和`_`. 还提供的`&`父选择标识符, 可以在嵌套中直接给父级添加伪类处理.
