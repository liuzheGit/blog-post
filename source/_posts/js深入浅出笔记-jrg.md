---
title: js深入浅出笔记-jrg
date: 2018-10-19 17:32:46
tags: JavaScript
categories: Front-End
---

# js深入浅出

## 你真的懂函数吗

- 匿名函数

  ```js
  var fn = function(){ //fn 是匿名函数的引用.
      console.log('fn')
  };

  var fn2 = fn;
  fn.name;  // fn
  fn2.name; // fn
  // 此时匿名函数是有name的
  ```

- 具名函数

  ```js
  function fn3(){ // 这是一个具名函数,如果这个具名函数的声名在 window
      return 3	//则 全局都可以访问
  }
  // 但是 如果像下面 把具名函数赋给一个变量 则它在window 访问是undefined
  var fn5 = function fn4(){};
  // 只是此时fn4 的 访问只能在 = 后 到 ; 前,
  ```

- 箭头函数

  ```js
  // 如果只有 一个 参数 且只有 return 语句
  var fn6 = i => i + 1;
  // 如果有多个 参数 则必须 括起来, 如果 不只有 return ,则必须用大括号括起来
  var fn6 = (x, y) => {
      console.log(x);
      return x + y;
  }
  ```



**js语义分析**

  抽象词法树

## stack 栈  先进先出

js是单线程的遇到函数就要进去执行,此时需要记住是在哪里进去的,这时候就像stack中添加一个记号,然后 函数执行完后,退出的时候,就从stack中取出这个记号,再往下执行.



### this 和 arguments

函数调用的最正确的方法

```js
fn.call();
// 其中call有两个参数,  第一个是 this.(必须是个对象,不传在浏览器中默认是window) 第二个是 arguments
```



- chrome的console.log 打印 fn.call() 的第一个参数this的时候 打印出来的是Window .其实是window
- this 就是call 的第一个参数 **记住**
- fn() 是阉割版的 fn.call();
- this必须是一个对象  它是函数和对象之间的羁绊
- 对象中的函数是独立的, 和对象没有一点关系, 只是js 在你用 对象.函数的时候自动把. 前面的对象 传给 call的第一个参数

### call / apply

- 如果你知道你的参数个数 则可以用call, 如果不知道有多少项 , 就使用 apply

### bind

> fn.bind.call(fn,{},1,2,3)

- call和apply 都是直接调用函数, 而 bind 则是返回一个函数 (return function)
- bind的作用实在你调用函数的后边加一个call , 不是现在加,而实在 调用这个新返回函数的时候加



### 柯里化 / 高阶函数

> 返回的函数的函数

- 柯里化：将 f(x,y) 变成 f(x=1)(y) 或 f(y=1)x

```
  //柯里化之前
  function sum(x,y){
      return x+y
  }
  //柯里化之后
  function addOne(y){
      return sum(1, y)
  }
  //柯里化之前
  function Handlebar(template, data){
      return template.replace('{{name}}', data.name)
  }
  //柯里化之后
  function Handlebar(template){
      return function(data){
          return template.replace('{{name}}', data.name)
      }
  }
```

- 柯里化可以将真实计算拖延到最后再做

  关于柯里化的高级文章：

  1. <http://www.yinwang.org/blog-cn/2013/04/02/currying>
  2. <https://zhuanlan.zhihu.com/p/31271179>

- 高阶函数：

  在数学和计算机科学中，高阶函数是至少满足下列一个条件的函数：

  1. 接受一个或多个函数作为输入：forEach sort map filter reduce

  2. 输出一个函数：lodash.curry

  3. 不过它也可以同时满足两个条件：Function.prototype.bind

### 数组的方法  是 高阶函数

- map

- filter

- reduce

- sort

- forEach

### 回调函数
> 名词形式：被当做参数的函数就是回调
> 动词形式：调用这个回调

> 回调和异步不是一回事

### 构造函数

> 返回对象的函数就是构造函数
> 一般首字母大写

### 箭头函数

> 不接受指定this(call)


