---
title: JavaScript基础复习6-Array
date: 2018-11-05 16:42:45
tags: JavaScript
categories: Front-End
---

## Array

`Array`作为构造函数，行为很不一致。因此，不建议使用它生成新数组，直接使用数组字面量是更好的做法。

```js
var a = new Array(3);
var b = [undefined, undefined, undefined];

a.length // 3
b.length // 3

a[0] // undefined
b[0] // undefined

0 in a // false
0 in b // true
```

上面代码中，`a`是一个长度为3的空数组，`b`是一个三个成员都是`undefined`的数组。读取键值的时候，`a`和`b`都返回`undefined`，但是`a`的键位都是空的，`b`的键位是有值的。

## 静态方法

### Array.isArray()

返回一个布尔值, 表示是否为数组. 可以弥补`typeof`的不足

```js
var arr = [1, 2, 3];
typeof arr // object
Array.isArray(arr) // true
```

## 实例方法

- `push` `pop`
- `shift` `unshift`
- `join`
- `concat`
- reverse
- `slice` 
- `splice`
- `sort`
- `map`
- `forEach`
- `filter`
- `some` `every`
- `reduce` `reduceRight`
- `indexOf` `lastIndexOf`

### 其中会改变原数组的有

push / pop / shift / unshift / reverse / splice / sort

### slice()

提取目标数组的一部分, 返回一个新数组, 原数组不变.

`arr.slice(start, end)` : 包前不包后原则; 如果没有参数,则返回一个原数组的拷贝;

es5的伪数组转数组:  为什么要转伪数组呢: 伪数组是类似数组形式的对象,但是没有数组实例的方法.

`Array.prototype.slice.call(likeArray)`



### splice()

用于删除原数组的一部分成员,并在删除的位置添加新的数组成员. 返回值是被删除的元素, 改变原数组.

第一个参数: 删除的起始位置(0开始), 第二个是被删除的个数, 后面依次是被添加的元素.

单纯的想插入元素可以把第二个参数设为0;

### sort()

排序默认是按照字典排序的, 原数组改变, 小到大;

如果想按照自定义的排序方式, 可以传入一个函数作为参数;

```js
var a = [10111, 1101, 111];

a.sort() // [10111, 1101, 111];

a.sort((a, b)=> a - b);  // [111, 1101, 10111]

```

上面代码中，`sort`的参数函数本身接受两个参数，表示进行比较的两个数组成员。如果该函数的返回值大于`0`，表示第一个成员排在第二个成员后面；其他情况下，都是第一个元素排在第二个元素前面。

### map()

`map`方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回, 原数组不变

`map`方法接受一个函数作为参数。该函数调用时，`map`方法向它传入三个参数：当前成员、当前位置和数组本身。

`map`还可以接受第二个参数, 用来绑定回调函数的`this`

```js
var arr = ['a', 'b', 'c'];

[1, 2].map(function (e) {
  return this[e];
}, arr)
// ['b', 'c']
```

`map`方法不会跳过`undefined`和`null`，但是会跳过空位。

### forEach()  - 可以被map替代, 

简单说和`map`类似, `forEach`方法不返回值，只用来操作数据。这就是说，如果数组遍历的目的是为了得到返回值，那么使用`map`方法，否则使用`forEach`方法。

- `forEach`方法无法中断执行

- `forEach`方法不会跳过`undefined`和`null`，但会跳过空位。



### filter()

`filter`方法用于过滤数组成员, 满足条件的成员组成新数组返回. 不改变原数组;

```js
var arr = [0, 1, 'a', false];

arr.filter(Boolean)
// [1, "a"]
```

上面代码中，`filter`方法返回数组`arr`里面所有布尔值为`true`的成员。

也可以接受第二个参数, 绑定this

### some() every()

返回一个布尔值, 表示判断数组成员是否符合某种条件;

它们接受一个函数作为参数，所有数组成员依次执行该函数。该函数接受三个参数：当前成员、当前位置和整个数组，然后返回一个布尔值。

`some`方法只要有一个成员返回`true`, 则`some`方法的返回值就是 `true`, 否则返回`false`;

`every`方法是所有成员的返回值都是`true`，整个`every`方法才返回`true`，否则返回`false`。

- 注意，对于空数组，`some`方法返回`false`，`every`方法返回`true`，回调函数都不会执行。
- `some`和`every`方法还可以接受第二个参数，用来绑定参数函数内部的`this`变量。

### reduce() reduceRight()

`reduce`方法和`reduceRight`方法依次处理数组的每个成员，最终累计为一个值。

一个从左到右, 一个相反.

```js
[1, 2, 3, 4, 5].reduce(function (a, b) {
  console.log(a, b);
  return a + b;
})
// 1 2
// 3 3
// 6 4
// 10 5
//最后结果：15
```

`reduce`方法和`reduceRight`方法的第一个参数都是一个函数。该函数接受以下四个参数。

1. 累积变量，默认为数组的第一个成员
2. 当前变量，默认为数组的第二个成员
3. 当前位置（从0开始）
4. 原数组

这四个参数之中，只有前两个是必须的，后两个则是可选的。

**第二参数可选, 代表累计变量的初值** : 处理空数组时尤其有用

```js
function add(prev, cur) {
  return prev + cur;
}

[].reduce(add)
// TypeError: Reduce of empty array with no initial value
[].reduce(add, 1)
// 1
```

上面代码中，由于空数组取不到初始值，`reduce`方法会报错。这时，加上第二个参数，就能保证总是会返回一个值。

由于这两个方法会遍历数组，所以实际上还可以用来做一些遍历相关的操作。比如，找出字符长度最长的数组成员。

```js
function findLongest(entries) {
  return entries.reduce(function (longest, entry) {
    return entry.length > longest.length ? entry : longest;
  }, '');
}

findLongest(['aaa', 'bb', 'c']) // "aaa"
```

上面代码中，`reduce`的参数函数会将字符长度较长的那个数组成员，作为累积值。这导致遍历所有成员之后，累积值就是字符长度最长的那个成员。



### indexOf() lastIndexOf()

`indexOf`方法返回给定元素在数组中第一次出现的位置，如果没有出现则返回`-1`

`indexOf`方法还可以接受第二个参数，表示搜索的开始位置

`lastIndexOf`方法返回给定元素在数组中最后一次出现的位置，如果没有出现则返回`-1`

- 注意，这两个方法不能用来搜索`NaN`的位置，即它们无法确定数组成员是否包含`NaN`
  - 这是因为这两个方法内部，使用严格相等运算符（`===`）进行比较，而`NaN`是唯一一个不等于自身的值。

## [参见](http://wangdoc.com/javascript/stdlib/array.html)


