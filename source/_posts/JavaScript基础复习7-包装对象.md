---
title: JavaScript基础复习7-包装对象
date: 2018-11-05 16:42:56
tags: JavaScript
categories: Front-End
---

# 包装对象 String Number Boolean

所谓“包装对象”，就是分别与数值、字符串、布尔值相对应的`Number`、`String`、`Boolean`三个原生对象。这三个原生对象可以把原始类型的值变成（包装成）对象。

`Number`、`String`和`Boolean`如果不作为构造函数调用（即调用时不加`new`），常常用于将任意类型的值转为数值、字符串和布尔值。

```js
Number(123) // 123
String('abc') // "abc"
Boolean(true) // true
```

总结一下，这三个对象作为构造函数使用（带有`new`）时，可以将原始类型的值转为对象；作为普通函数使用时（不带有`new`），可以将任意类型的值，转为原始类型的值。



## String

**静态方法** -- 定义在对象本身，而不是定义在对象实例的方法



**实例方法**

### concat()

连接两个字符串, 返回一个新的字符串, 不改变原字符串;

### slice()

`slice`方法用于从原字符串取出字符串并返回. 不改变原字符串; 包前不包后原则;

### substring() 不推荐

`substring`方法用于从原字符串取出子字符串并返回，不改变原字符串，跟`slice`方法很相像。它的第一个参数表示子字符串的开始位置，第二个位置表示结束位置（返回结果不含该位置）。

不建议使用, 优先使用`slice`

### substr()

`substr`方法用于从原字符串取出子字符串并返回，不改变原字符串;和 `slice` 和`substring`作用一样, 但是第二个参数是 截取的个数.

- 如果省略第二个参数，则表示子字符串一直到原字符串的结束。
- 如果第一个参数是负数，表示倒数计算的字符位置。如果第二个参数是负数，将被自动转为0，因此会返回空字符串。

### indexOf() lastIndexOf()

`indexOf`方法用于确定一个字符串在另一个字符串中第一次出现的位置，返回结果是匹配开始的位置。如果返回`-1`，就表示不匹配。 第二个参数表示从该位置开始;



### trim()

去除字符串两端的空格. 返回新的, 不改变原来的;

该方法去除的不仅是空格，还包括制表符（`\t`、`\v`）、换行符（`\n`）和回车符（`\r`）。



### toLowerCase() toUpperCase()

`toLowerCase`方法用于将一个字符串全部转为小写，`toUpperCase`则是全部转为大写。它们都返回一个新字符串，不改变原字符串。

### split()

`split`方法按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组



## Math

`Math`对象的静态属性，提供以下一些数学常数。

- `Math.E`：常数`e`。
- `Math.LN2`：2 的自然对数。
- `Math.LN10`：10 的自然对数。
- `Math.LOG2E`：以 2 为底的`e`的对数。
- `Math.LOG10E`：以 10 为底的`e`的对数。
- `Math.PI`：常数`π`。
- `Math.SQRT1_2`：0.5 的平方根。
- `Math.SQRT2`：2 的平方根。



`Math`对象提供以下一些静态方法。

- `Math.abs()`：绝对值
- `Math.ceil()`：向上取整
- `Math.floor()`：向下取整
- `Math.max()`：最大值, 参数中的最大值
- `Math.min()`：最小值
- `Math.pow()`：指数运算
- `Math.sqrt()`：平方根
- `Math.log()`：自然对数
- `Math.exp()`：`e`的指数
- `Math.round()`：四舍五入
- `Math.random()`：随机数



## Number

### `toString()`

`toString`方法可以接受一个参数，表示输出的进制。

### `toFixed()`

`toFixed`方法先将一个数转为指定位数的小数，然后返回这个小数对应的字符串。

### `toExponential`()

`toExponential`方法用于将一个数转为科学计数法形式。

### `toPrecision()`

`toPrecision`方法用于将一个数转为指定位数的有效数字。
