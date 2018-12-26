---
title: JavaScript基础复习4-标准库
date: 2018-11-05 16:40:32
tags: JavaScript
categories: Front-End
---

# Object对象

JavaScript原生提供的`Object`.其他对象都继承自`Object`对象.

`Object`对象的原生方法分成两类：`Object`本身的方法与`Object`的实例方法。

- 本身的方法: 定义在Object对象的方法

  `Object.print = function (o) { console.log(o) };`

- 实例方法: 定义在Object.prototype 原型的方法, 可以被实例直接使用

## Object()

本身是一个函数, 如果参数是空, 则返回空对象;

- `Object`函数的参数是各种原始类型的值，转换成对象就是原始类型值对应的包装对象。

- 如果`Object`方法的参数是一个对象，它总是返回该对象，即不用转换。

  利用这一点，可以写一个判断变量是否为对象的函数。

  ```js
  function isObjcet(value){
      if (value === Object(value)){
          return true;
      } else{
          return false
      }
  }
  isObject([]); // true
  isObject(false); // false
  ```


### 验证实例是否是构造函数的实例 - instanceof

`instanceof`运算符用来验证，一个对象是否为指定的构造函数的实例。`obj instanceof Object`返回`true`，就表示`obj`对象是`Object`的实例。



## Object 构造函数

`Object`构造函数的首要用途，是直接通过它来生成新对象。

> 注意，通过`var obj = new Object()`的写法生成新对象，与字面量的写法`var obj = {}`是等价的。或者说，后者只是前者的一种简便写法。



## Object 和 new Object

用法相似,但两者作用完全不同, `Object(value)`是将value转化为对象, `new Object(value)`,则表示生成一个对象, 值是value;



## Object的静态方法

所谓“静态方法”，是指部署在`Object`对象自身的方法。

### `Object.keys()` 和`Object.getOwnPropretyNames()`

都是用来遍历对象属性的. 括号中是要遍历的对象, 返回一个数组,包含对象自身的属性. 一般来说二者返回的是一样的,只有涉及不可枚举对象时, `keys() `只返回可以枚举的, 另一个还返回不可枚举的.

> 一般使用`keys()`, 获取属性个数可以`Object.keys().length`



## Object的实例方法

定义在`Object.prototype`的方法,可以被每个实例直接使用的方法.

### `Object.prototype.valueOf`

`valueOf`方法的作用是返回一个对象的“值”，默认情况下返回对象本身。`valueOf`方法的主要用途
是，JavaScript 自动类型转换时会默认调用这个方法.



### `Object.prototype.toString`

`toString`方法的作用是返回一个对象的字符串形式，默认情况下返回类型字符串。

> 对于一个对象调用`toString`方法，会返回字符串`[object Object]`，该字符串说明对象的类型。

**数组、字符串、函数、Date 对象都分别部署了自定义的`toString`方法，覆盖了`Object.prototype.toString`方法。**

```js
[1, 2, 3].toString() // "1,2,3"

'123'.toString() // "123"

(function () {
  return 123;
}).toString()
// "function () {
//   return 123;
// }"

(new Date()).toString()
// "Tue May 10 2016 09:11:31 GMT+0800 (CST)"
```

由此可见, 为了防止自定义`toString`属性, 覆盖掉`Object.prototype.toString`方法，所以为了得到类型字符串，最好直接使用`Object.prototype.toString`方法。通过函数的`call`方法，可以在任意值上调用这个方法，帮助我们判断这个值的类型。

`Object.prototype.toString.call(value)`

上面的方法,不同数据类型的`Object.prototype.toString`方法返回值如下。

- 数值：返回`[object Number]`。
- 字符串：返回`[object String]`。
- 布尔值：返回`[object Boolean]`。
- undefined：返回`[object Undefined]`。
- null：返回`[object Null]`。
- 数组：返回`[object Array]`。
- arguments 对象：返回`[object Arguments]`。
- 函数：返回`[object Function]`。
- Error 对象：返回`[object Error]`。
- Date 对象：返回`[object Date]`。
- RegExp 对象：返回`[object RegExp]`。
- 其他对象：返回`[object Object]`。

这就是说，`Object.prototype.toString`可以看出一个值到底是什么类型。

**利用这个特性，可以写出一个比`typeof`运算符更准确的类型判断函数。**

```js
var type = function (o){
  var s = Object.prototype.toString.call(o);
  return s.match(/\[object (.*?)\]/)[1].toLowerCase();
};

type({}); // "object"
type([]); // "array"
type(5); // "number"
type(null); // "null"
type(); // "undefined"
type(/abcd/); // "regex"
type(new Date()); // "date"
```

## [详见](http://wangdoc.com/javascript/stdlib/object.html)
