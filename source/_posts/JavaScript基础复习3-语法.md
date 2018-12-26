---
title: JavaScript基础复习3-语法
date: 2018-10-29 16:56:35
tags: JavaScript
categories: Front-End
---

## 数据类型的转换

JavaScript 是一种动态类型语言，变量没有类型限制，可以随时赋予任意值。

### 强制转换 (Number(), String(), Bookean())

#### Number()

1. 原始类型

2. ```js
   // 数值：转换后还是原来的值
   Number(324) // 324
   
   // 字符串：如果可以被解析为数值，则转换为相应的数值
   Number('324') // 324
   
   // 字符串：如果不可以被解析为数值，返回 NaN
   Number('324abc') // NaN
   
   // 空字符串转为0
   Number('') // 0
   
   // 布尔值：true 转成 1，false 转成 0
   Number(true) // 1
   Number(false) // 0
   
   // undefined：转成 NaN
   Number(undefined) // NaN
   
   // null：转成0
   Number(null) // 0
   ```

2. 对象: `Number`方法的参数是对象时，将返回`NaN`，除非是包含单个数值的数组。

3. ```js
   Number({a: 1}) // NaN
   Number([1, 2, 3]) // NaN
   Number([5]) // 5
   ```

#### String()

1. 原始类型

   - **数值**：转为相应的字符串。
   - **字符串**：转换后还是原来的值。
   - **布尔值**：`true`转为字符串`"true"`，`false`转为字符串`"false"`。
   - **undefined**：转为字符串`"undefined"`。
   - **null**：转为字符串`"null"`。

2. 对象 :参数如果是对象，返回一个类型字符串；如果是数组，返回该数组的字符串形式。

3. ```js
   String({a: 1}) // "[object Object]"
   String([1, 2, 3]) // "1,2,3"
   ```

#### Boolean()

除了以下五个值的转换结果为`false`，其他的值全部为`true`。

- `undefined`
- `null`
- `-0`或`+0`
- `NaN`
- `''`（空字符串）

**注意，所有对象（包括空对象）的转换结果都是`true`，甚至连`false`对应的布尔对象`new Boolean(false)`也是`true`**

#### 自动转换

**由于自动转换具有不确定性**，而且不易除错，建议在预期为布尔值、数值、字符串的地方，全部使用`Boolean`、`Number`和`String`函数进行显式转换。



## 错误处理机制

JavaScript 原生提供`Error`构造函数，所有抛出的错误都是这个构造函数的实例。

### 原生错误类型

`Error`实例对象是最一般的错误类型, 在它的基础上, JavaScript还定义了其他6种错误对象: 

1. SyntaxError : 语法错误
2. RefrenceError: 引用一个不存在的变量的错误
   - 另一种触发场景是，将一个值分配给无法分配的对象，比如对函数的运行结果或者`this`赋值。
3. RangeError: 一个超出有效范围时的错误, 有几种: 
   - 数组长度为负
   - `Number`对象的参数超出范围
   - 函数堆栈超过最大值
4. TypeError: 对象是变量或参数不是预期类型时发生的错误。
5. URIErrorURI 相关函数的参数不正确时抛出的错误
6. EvalError对象: `eval`函数没有被正确执行时，会抛出`EvalError`错误 (已不再使用)

### throw语句

`throw`语句的作用是手动中断程序执行，抛出一个错误。有错程序就会中断;

### try...catch结构

简单说就是在try语句中抛出的错误会被后面的catch语句所捕获, 并且把错误当作参数传给catch;

```js
try {
  throw new Error('出错了!');
} catch (e) {
  console.log(e.name + ": " + e.message);
  console.log(e.stack);
}
// Error: 出错了!
//   at <anonymous>:3:9
//   ...
```

`catch`代码块捕获错误之后，程序不会中断，会按照正常流程继续执行下去。

`catch`代码块之中，还可以再抛出错误，甚至使用嵌套的`try...catch`结构。

为了捕捉不同类型的错误，`catch`代码块之中可以加入判断语句。

### finally代码块

`try...catch`结构允许在最后添加一个`finally`代码块，表示不管是否出现错误，都必需在最后运行的语句。



## 编码风格

- 建议总是使用大括号表示区块。

- 用空格区分不同的括号 

  - 函数调用不要空格

  - 表达式间用空格

    - 表示函数调用时，函数名与左括号之间没有空格。

    - 表示函数定义时，函数名与左括号之间没有空格。

    - 其他情况时，前面位置的语法元素与左括号之间，都有一个空格。

- 分号表示一条语句的结束, 所以不要省略结尾的分号;

- 不使用分号的情况

  - for和while循环 结尾没有分号
  - if, switch, try 结尾没有分号
  - 函数声明 没有分号

- 避免全局变量, 不得不用时, 用首字母大写区分;

- for () 循环 的 空号内部如果用 var i = 0; 会产生一个全局的变量i

- 比较用 `===`严格相等

- 所有的`++`运算符都可以用`+= 1`代替

- `switch...case`结构要求在每个`case`的最后一行必须是 `break`语句;

## console对象和控制台

### console

> `console`对象是 JavaScript 的原生对象

### console.log() , console.info()

`console.log`方法的第一个参数有三个占位符（`%s`），第二、三、四个参数会在显示时，依次替换掉这个三个占位符。

`console.log`方法支持以下占位符，不同类型的数据必须使用对应的占位符。

- `%s` 字符串
- `%d` 整数
- `%i` 整数
- `%f` 浮点数
- `%o` 对象的链接
- `%c` CSS 格式字符串

`console.info`是`console.log`方法的别名，用法完全一样。只不过`console.info`方法会在输出信息的前面，加上一个**蓝色图标**。

`console.debug`方法与`console.log`方法类似，会在控制台输出调试信息。但是，默认情况下，`console.debug`输出的**信息不会显示**，只有在打开显示级别在`verbose`的情况下，才会显示。

### console.warn()，console.error()

`warn`方法和`error`方法也是在控制台输出信息，它们与`log`方法的不同之处在于，`warn`方法输出信息时，在最前面加一个**黄色三角**，表示警告；`error`方法输出信息时，在最前面加一个**红色的叉**，表示出错。同时，还会高亮显示输出文字和错误发生的堆栈。其他方面都一样。

### console.table()

对于复合类型的数据, `console.table` 方法可以将其转为**表格显示**.

### console.count()

`count`方法用于计数，输出它被调用了多少次。

### console.dir()，console.dirxml()

`dir`方法用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示。

### console.assert()

`console.assert`方法主要用于程序运行过程中，进行条件判断，如果不满足条件，就显示一个错误，但不会中断程序执行。这样就相当于提示用户，内部状态不正确。

### console.time()，console.timeEnd() 

这两个方法用于计时，可以算出一个操作所花费的准确时间。

```js
console.time('Array initialize');

var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};

console.timeEnd('Array initialize');
// Array initialize: 1914.481ms
```

`time`方法表示计时开始，`timeEnd`方法表示计时结束。它们的参数是计时器的名称。调用`timeEnd`方法之后，控制台会显示“计时器名称: 所耗费的时间”。



### console.group()，console.groupEnd()，console.groupCollapsed()

`console.group`和`console.groupEnd`这两个方法用于将显示的信息分组。它只在输出大量信息时有用，分在一组的信息，可以用鼠标折叠/展开

### console.trace()，console.clear()

`console.trace`方法显示当前执行的代码在堆栈中的调用路径。

`console.clear`方法用于清除当前控制台的所有输出.

### 控制台命令行API

#### `$_`

返回上一个表达式的值

#### `$0`-`$4`

控制台保存了最近5个在 Elements 面板选中的 DOM 元素，`$0`代表倒数第一个（最近一个），`$1`代表倒数第二个，以此类推直到`$4`。

#### `$(selector)`

`$(selector)`返回第一个匹配的元素，等同于`document.querySelector()`。如果页面脚本中有`$`的定义,则会覆盖,如 jquery,则会用jqeury实现的;

#### `$(selector)`

`$$(selector)`返回选中的 DOM 对象，等同于`document.querySelectorAll`。

#### `$x(path)`

`$x(path)`方法返回一个数组，包含匹配特定 XPath 表达式的所有 DOM 元素

#### `inspect(object)`

`inspect(object)`方法打开相关面板，并选中相应的元素，显示它的细节。如`inspect(document)`会在Elements面板显示`document`元素

#### keys(object)`，`values(object)

`keys(object)`方法返回一个数组，包含`object`的所有键名。

`values(object)`方法返回一个数组，包含`object`的所有键值。

#### 其他方法:

命令行 API 还提供以下方法。

- `clear()`：清除控制台的历史。
- `copy(object)`：复制特定 DOM 元素到剪贴板。
- `dir(object)`：显示特定对象的所有属性，是`console.dir`方法的别名。
- `dirxml(object)`：显示特定对象的 XML 形式，是`console.dirxml`方法的别名。

#### debugger 语句

`debugger`语句主要用于除错，作用是设置断点。如果有正在运行的除错工具，程序运行到`debugger`语句时会自动停下。如果没有除错工具，`debugger`语句不会产生任何结果，JavaScript 引擎自动跳过这一句。

Chrome 浏览器中，当代码运行到`debugger`语句时，就会暂停运行，自动打开脚本源码界面。

## 具体查看 [console](http://wangdoc.com/javascript/features/console.html)

