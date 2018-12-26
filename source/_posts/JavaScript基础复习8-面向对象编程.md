---
title: JavaScript基础复习8-面向对象编程
date: 2018-11-05 16:43:59
tags: JavaScript
categories: Front-End
---

- 为了与普通函数区别，构造函数名字的第一个字母通常大写
  - 函数体内部使用`this`关键字, 代表了所要生成的对象的实例
  - 生成对象的时候, 必须使用`new`命令
- `new`命令执行构造函数, 推荐后面加括号`var v = new V()`
- 避免不使用`new`命令、直接调用构造函数

## new的原理

使用`new`命令时，它后面的函数依次执行下面的步骤。

1. 创建一个空对象，作为将要返回的对象实例。
2. 将这个空对象的原型，指向构造函数的`prototype`属性。
3. 将这个空对象赋值给函数内部的`this`关键字。
4. 开始执行构造函数内部的代码。

- 构造函数内部`this`指的是新创建的空对象
- 如果内部有return ,且返回一个对象,则 构造函数返回这个手动返回的对象, 如果没有return 或者return的不是一个对象, 则会被忽略
- 如果`return`语句返回的是一个跟`this`无关的新对象，`new`命令会返回这个新对象，而不是`this`对象。这一点需要特别引起注意
- 如果对普通函数（内部没有`this`关键字的函数）使用`new`命令，则会返回一个空对象
- 这是因为`new`命令总是返回一个对象，要么是实例对象，要么是`return`语句指定的对象。

`new`命令简化的内部流程，可以用下面的代码表示。

```js
function _new(/* 构造函数 */ constructor, /* 构造函数参数 */ params) {
  // 将 arguments 对象转为数组
  var args = [].slice.call(arguments);
  // 取出构造函数
  var constructor = args.shift();
  // 创建一个空对象，继承构造函数的 prototype 属性
  var context = Object.create(constructor.prototype);
  // 执行构造函数
  var result = constructor.apply(context, args);
  // 如果返回结果是对象，就直接返回，否则返回 context 对象
  return (typeof result === 'object' && result != null) ? result : context;
}

// 实例
var actor = _new(Person, '张三', 28);
```

### 没有用new调用构造函数的处理

1. new.target法

   ```js
   function f() {
     if (!new.target) {
       throw new Error('请使用 new 命令调用！');
     }
     // ...
   }
   
   f() // Uncaught Error: 请使用 new 命令调用！
   ```

2. 内部用严格模式

   ```js
   function Fubar(foo, bar){
     'use strict';
     this._foo = foo;
     this._bar = bar;
   }
   
   Fubar()
   // TypeError: Cannot set property '_foo' of undefined
   ```

3. 返回new调用

   ```js
   function Fubar(foo, bar) {
     if (!(this instanceof Fubar)) {
       return new Fubar(foo, bar);
     }
   
     this._foo = foo;
     this._bar = bar;
   }
   
   Fubar(1, 2)._foo // 1
   (new Fubar(1, 2))._foo // 1
   ```

4. instanceof法

   ```js
   function Fubar (foo, bar) {
     if (this instanceof Fubar) {
       this._foo = foo;
       this._bar = bar;
     } else {
       return new Fubar(foo, bar);
     }
   }
   ```


## object.create()

没有构造函数, 用现有的对象作为模板,生成实例:

```js
var person1 = {
  name: '张三',
  age: 38,
  greeting: function() {
    console.log('Hi! I\'m ' + this.name + '.');
  }
};

var person2 = Object.create(person1);

person2.name // 张三
person2.greeting() // Hi! I'm 张三.
```

`person1`是`person2`的模板, 后者继承的前者的属性和方法.



## this

`this`都有一个共同点：它总是返回一个对象

由于对象的属性可以赋给另一个对象，所以属性所在的当前对象是可变的，即`this`的指向是可变的。

如果`this`所在的方法不在对象的第一层，这时`this`只是指向当前一层的对象，而不会继承更上面的层。

```js
var a = {
  p: 'Hello',
  b: {
    m: function() {
      console.log(this.p);
    }
  }
};

a.b.m() // undefined
```

上面代码中，`a.b.m`方法在`a`对象的第二层，该方法内部的`this`不是指向`a`，而是指向`a.b`，因为实际执行的是下面的代码。

- 使用一个变量固定`this`的值，然后内层函数调用这个变量，是非常常见的做法
- JavaScript 提供了严格模式，也可以硬性避免这种问题。严格模式下，如果函数内部的`this`指向顶层对象，就会报错

### 绑定this的方法

avaScript 提供了`call`、`apply`、`bind`这三个方法，来切换/固定`this`的指向。

> `call`和`apply`都会立即执行, 而`bind`则返回一个新的函数

#### call()

- `call`方法的参数，应该是一个对象。如果参数为空、`null`和`undefined`，则默认传入全局对象。

- 如果`call`方法的参数是一个原始值，那么这个原始值会自动转成对应的包装对象，然后传入`call`方法

`call`方法的一个应用是调用对象的原生方法。

```js
var obj = {};
obj.hasOwnProperty('toString') // false

// 覆盖掉继承的 hasOwnProperty 方法
obj.hasOwnProperty = function () {
  return true;
};
obj.hasOwnProperty('toString') // true

Object.prototype.hasOwnProperty.call(obj, 'toString') // false
```

上面代码中，`hasOwnProperty`是`obj`对象继承的方法，如果这个方法一旦被覆盖，就不会得到正确结果。`call`方法可以解决这个问题，它将`hasOwnProperty`方法的原始定义放到`obj`对象上执行，这样无论`obj`上有没有同名方法，都不会影响结果。

#### apply()

和`call`类似, 它接收一个数组作为函数执行时的参数

**用处**

1. **将数组的空元素变为undefined**

   通过`apply`方法，利用`Array`构造函数将数组的空元素变成`undefined`。

   ```js
   Array.apply(null, ['a', ,'b'])
   // [ 'a', undefined, 'b' ]
   ```

   空元素与`undefined`的差别在于，数组的`forEach`方法会跳过空元素，但是不会跳过`undefined`。

2. **转换类似数组的对象**

   另外，利用数组对象的`slice`方法，可以将一个类似数组的对象（比如`arguments`对象）转为真正的数组。

   ```js
   Array.prototype.slice.apply({0: 1, length: 1}) // [1]
   Array.prototype.slice.apply({0: 1}) // []
   Array.prototype.slice.apply({0: 1, length: 2}) // [1, undefined]
   Array.prototype.slice.apply({length: 1}) // [undefined]
   ```

   上面代码的`apply`方法的参数都是对象，但是返回结果都是数组，这就起到了将对象转成数组的目的。从上面代码可以看到，这个方法起作用的前提是，被处理的对象必须有`length`属性，以及相对应的数字键。

#### bind()

`bind`方法用于将函数体内的`this`绑定到某个对象，然后返回一个新函数

### [参见](http://wangdoc.com/javascript/oop/this.html)



## 对象的继承

### 原型链

读取对象的某个属性时，JavaScript 引擎先寻找对象本身的属性，如果找不到，就到它的原型去找，如果还是找不到，就到原型的原型去找。如果直到最顶层的`Object.prototype`还是找不到，则返回`undefined`。如果对象自身和它的原型，都定义了一个同名属性，那么优先读取对象自身的属性，这叫做“覆盖”（overriding）。

### constructor

修改原型对象时，一般要同时修改`constructor`属性的指向

### instanceof

返回一个布尔值, 表示对象是否是某个构造函数的实例.

```js
var v = new Vehicle();
v instanceof Vehicle // true
```

由于`instanceof`检查整个原型链，因此同一个实例对象，可能会对多个构造函数都返回`true`。

`instanceof`运算符的一个用处，是判断值的类型

```js
var x = [1, 2, 3];
var y = {};
x instanceof Array // true
y instanceof Object // true
```

只适用于对象, 不适用于原始类型的值. 如 String .

对于`undefined`和`null`, `instanceof`总返回`false`;



## 构造函数的继承

分两步: 

```js
// 第一步: 在子类的构造函数中调用父类的构造函数, 让子类实例具有父类实例的属性;
function Sub(){
  Super.call(this);
}

// 第二步: 让子类的原型指向父类的原型, 子类继承父类;
Sub.prototype = Object.create(Super.prototype);
Sub.prototype.constructor = Sub;
```

## [参见](http://wangdoc.com/javascript/oop/prototype.html)

## Object.create()

`Object.create(Super)`

该方法接受一个对象作为参数, 然后以它为原型,  返回一个实例对象. 该实例完全继承原型对象的属性.

下面三种方式生成的新对象是等价的。

```js
var obj1 = Object.create({});
var obj2 = Object.create(Object.prototype);
var obj3 = new Object();
```

如果想生成的对象没有任何属性. 将Object.create的参数设为`null`;

- 必须给定参数, 且不能是非对象
- `Object.create`方法生成的新对象，动态继承了原型

### in 运算符 和 for ... in 循环

`in`运算符返回一个布尔值, 表示一个对象是否具有某个属性. 继承的也返回`true`

- `in`运算符常用于检查一个属性是否存在

获得对象的所有可遍历属性（不管是自身的还是继承的），可以使用`for...in`循环

为了在`for...in`循环中获得对象自身的属性，可以采用`hasOwnProperty`方法判断一下。

```js
for ( var name in object ) {
  if ( object.hasOwnProperty(name) ) {
    /* loop code */
  }
}
```

## 对象的拷贝

如果要拷贝一个对象，需要做到下面两件事情。

- 确保拷贝后的对象，与原对象具有同样的原型。
- 确保拷贝后的对象，与原对象具有同样的实例属性。

下面就是根据上面两点，实现的对象拷贝函数。

```js
function copyObject(orig) {
  var copy = Object.create(Object.getPrototypeOf(orig));
  copyOwnPropertiesFrom(copy, orig);
  return copy;
}

function copyOwnPropertiesFrom(target, source) {
  Object
    .getOwnPropertyNames(source)
    .forEach(function (propKey) {
      var desc = Object.getOwnPropertyDescriptor(source, propKey);
      Object.defineProperty(target, propKey, desc);
    });
  return target;
}
```

另一种更简单的写法，是利用 ES2017 才引入标准的`Object.getOwnPropertyDescriptors`方法。

```js
function copyObject(orig) {
  return Object.create(
    Object.getPrototypeOf(orig),
    Object.getOwnPropertyDescriptors(orig)
  );
}
```

## 严格模式 es5引入

`'use strict';`

### 启用方法

1. 可在整段的script中
2. 可以在函数function中

必须放在第一行,否则失效;(第一行可以是在注释后)



### 显式报错

> 以下情况会报错

- 设置字符串`length`属性
- 对只读属性赋值, 或者删除不可配置属性
- 只有getter, 没有setter
- 对禁止扩展的对象添加新属性
- 使用`eval`和`arguments`作为标识名
- 函数有重名函数
- 八进制的前缀`0`表示法
- 变量没有声名,即使用,(正常模式中, 如果一个变量没有声名就赋值,默认是全局变量)
- `this`关键字指向全局对象 
- 禁止使用 fn.callee、fn.caller
- 禁止使用 arguments.callee / arguments.caller
- 禁止删除变量