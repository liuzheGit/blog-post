---
title: JavaScript基础复习1-前言+数据类型
date: 2018-10-28 22:02:02
tags: JavaScript
categories: Front-End
---
# 要点

## 前言和基础语法

- 脚本语言:不具备编写操作系统的能力

- JavaScript 也是一种嵌入式（embedded）语言。

- 变量就是给值起名

- JavaScript引擎的工作方式是:先解释代码.在一行行执行.

- ```js
  var a;
  console.log(a);
  a = 1;
  // 结果是显示undefined 表示变量a 已声明但还未赋值
  ```

- 标识符, JavaScript引擎遇到非法标识符就会报错

- 标识符命名规则如下。

  - 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（`$`）和下划线（`_`）。

  - 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字`0-9`。

  - 中文是合法的标识符,可以作为变量名

  - > JavaScript 有一些保留字，不能用作标识符：arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield。

- 注释: 源码中被 JavaScript 引擎忽略的部分就叫做注释

  - 单行注释: `//`
  - 多行注释放到: `/*`和`*/`之间

- 由于历史上 JavaScript 可以兼容 HTML 代码的注释，所以`<!--`和`-->`也被视为合法的单行注释。

- 需要注意的是，`-->`只有在行首，才会被当成单行注释，否则会当作正常的运算。

  - ```js
    n --> 0`实际上会当作`n-- > 0
    ```

- 对于`var`命令来说，JavaScript 的区块`{}`不构成单独的作用域（scope）。

  - 区块往往用来构成其他更复杂的语法结构，比如`for`、`if`、`while`、`function`等。

- if 结构 是根据一个布尔值执行不同的语句, "布尔值"往往由一个条件表达式产生, 必须放在圆括号中,表示对表达式求值.

- 三元运算符: `(条件)? {表达式1}:{表达式2}` 条件为true ,执行表达式1 ,否则执行表达式2

  - ```js
      var msg = '数字' + n + '是' + (n % 2 === 0 ? '偶数' : '奇数');
      ```

- for循环

  - `for`语句后面的括号里面，有三个表达式。
    - 初始化表达式（initialize）：确定循环变量的初始值，只在循环开始时执行一次。
    - 条件表达式（test）：每轮循环开始时，都要执行这个条件表达式，只有值为真，才继续进行循环。
    - 递增表达式（increment）：每轮循环的最后一个操作，通常用来递增循环变量。

- do...while需要注意

  - `do...while`循环至少运行一次，这是这种结构最大的特点
  - `while`语句后面的分号注意不要省略

- `break`语句用于跳出代码块或循环。

- `continue`语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。

- break和continue注意: 如果存在多重循环，不带参数的`break`语句和`continue`语句都只针对最内层循环。

- **标签(label)**JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置，标签的格式如下。:

  ```js
  label:
    语句
  ```

  - 标签通常与`break`语句和`continue`语句配合使用，跳出特定的循环
  - 示例 : [阮一峰JavaScript-基础语法](http://wangdoc.com/javascript/basic/grammar.html)

## 数据类型

> JavaScript有7中数据类型: number(数值), string(字符串), boolean(布尔值), null, undefined, object(对象), Symbol

- 数值和字符串和布尔值 合成为 原始类型,他们最基本,无法再细分了.

- 对象称为合成类型的值,因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。

- `undefined`和`null`可以看成是两个特殊值

- 对象分为三个子类:

  - 狭义的对象(object)
  - 数组(array)
  - 函数(function)

  > 函数其实是处理数据的方法，JavaScript 把它当成一种数据类型，可以赋值给变量，这为编程带来了很大的灵活性，也为 JavaScript 的“函数式编程”奠定了基础。

- `typeof`运算符可以返回一个值的数据类型。

  - 数值、字符串、布尔值分别返回`number`、`string`、`boolean`。

  - 函数返回`function`

  - `undefined`返回`undefined`

  - `NaN` 返回 `number`

  - 利用这一点，`typeof`可以用来检查一个没有声明的变量，而不报错。

  - ```js
    v
    // ReferenceError: v is not defined
    
    typeof v
    // "undefined"
    
    // 错误的写法
    if (v) {
      // ...
    }
    // ReferenceError: v is not defined
    
    // 正确的写法
    if (typeof v === "undefined") {
      // ...
    }
    ```

  - 对象返回`object`

  - `null`返回 `object`

  - ```js
    typeof window // "object"
    typeof {} // "object"
    typeof [] // "object"
    ```

  - 数组也是`object` 是一种特殊的对象. `instanceof`可以判断是否是数组

  - ```js
    var o = {};
    var a = [];
    
    o instanceof Array // false
    a instanceof Array // true
    ```

### null-undefined-boolean

- `null`是一个表示“空”的对象，转为数值时为`0`；`undefined`是一个表示"此处无定义"的原始值，转为数值时为`NaN`。
- 函数无返回值时, 默认返回`undefined`
- 下列运算符会返回布尔值：
  - 前置逻辑运算符： `!` (Not)
  - 相等运算符：`===`，`!==`，`==`，`!=`
  - 比较运算符：`>`，`>=`，`<`，`<=`
- 以下6个值会被JavaScript引擎自动转化为布尔值时,转为false,其他的都是true
  - `undefined`
  - `null`
  - `false`
  - `0`
  - `' '`或`" "`(空字符串)
  - `NaN`
- 空数组`[]`和空对象`{}`都是`true`

## 数值

- JavaScript 对整数提供四种进制的表示方法：十进制、十六进制、八进制、二进制。

  - 十进制: 没有前导0的数值

  - 八进制：有前缀`0o`或`0O`的数值，或者有前导0、且只用到0-7的八个阿拉伯数字的数值。

  - 十六进制：有前缀`0x`或`0X`的数值。

  - 二进制：有前缀`0b`或`0B`的数值。

  - > 默认情况下，JavaScript 内部会自动将八进制、十六进制、二进制转为十进制。

- `NaN`是 JavaScript 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。

- ```js
  5 - 'x' // NaN
  ```

- `0`除以`0`也会得到`NaN`。

- `Infinity`表示“无穷”，用来表示两种场景。一种是一个正的数值太大，或一个负的数值太小，无法表示；另一种是非0数值除以0，得到`Infinity`。

### 与数值相关的全局方法

- `parseInt`方法用于将字符串转为整数

  - 如果字符串头部有空格，空格会被自动去除

  - 字符串转为整数的时候，是一个个字符依次转换，如果遇到不能转为数字的字符，就不再进行下去，返回已经转好的部分。
  - 如果`parseInt`的参数不是字符串，则会先转为字符串再转换。
  - 如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回`NaN`。
- `parseInt`还接受第二个参数(默认是十进制), 表示被解析的值得进制
- `parseFloat`方法用于将一个字符串转为浮点数

  - `parseFloat`会将空字符串转为`NaN`
  - 如果字符串包含不能转为浮点数的字符，则不再进行往后转换，返回已经转好的部分。
- `isFinite`方法返回一个布尔值，表示某个值是否为正常的数值。
  - 除了`Infinity`、`-Infinity`、`NaN`和`undefined`这几个值会返回`false`，`isFinite`对于其他的数值都会返回`true`。

## 字符串

> 由于 HTML 语言的属性值使用双引号，所以很多项目约定 JavaScript 语言的字符串只使用单引号.当然，只使用双引号也完全可以。重要的是坚持使用一种风格，不要一会使用单引号表示字符串，一会又使用双引号表示。

- 字符串如果想要输入多行, 可以在每一行尾部使用 反斜杠 `\`,但是输出还是单行的

- 如果想输出多行字符串，有一种利用多行注释的变通方法。

- ```js
  (function () { /*
  line 1
  line 2
  line 3
  */}).toString().split('\n').slice(1, -1).join('\n')
  // "line 1
  // line 2
  // line 3"
  ```

- 反斜杠（\）在字符串内有特殊含义，用来表示一些特殊字符，所以又称为转义符。

- 需要用反斜杠转义的特殊字符，主要有下面这些。

  - `\0` ：null（`\u0000`）
  - `\b` ：后退键（`\u0008`）
  - `\f` ：换页符（`\u000C`）
  - `\n` ：换行符（`\u000A`）
  - `\r` ：回车键（`\u000D`）
  - `\t` ：制表符（`\u0009`）
  - `\v` ：垂直制表符（`\u000B`）
  - `\'` ：单引号（`\u0027`）
  - `\"` ：双引号（`\u0022`）
  - `\\` ：反斜杠（`\u005C`）

- 反斜杠还有三种特殊用法。

  （1）`\HHH`

  反斜杠后面紧跟三个八进制数（`000`到`377`），代表一个字符。`HHH`对应该字符的 Unicode 码点，比如`\251`表示版权符号。显然，这种方法只能输出256种字符。

  （2）`\xHH`

  `\x`后面紧跟两个十六进制数（`00`到`FF`），代表一个字符。`HH`对应该字符的 Unicode 码点，比如`\xA9`表示版权符号。这种方法也只能输出256种字符。

  （3）`\uXXXX`

  `\u`后面紧跟四个十六进制数（`0000`到`FFFF`），代表一个字符。`XXXX`对应该字符的 Unicode 码点，比如`\u00A9`表示版权符号。

- 如果在非特殊字符前面使用反斜杠，则反斜杠会被省略

- 转义符转义自身`\\` 输出`\`

- 字符串可以被视为字符数组，因此可以使用数组的方括号运算符，用来返回某个位置的字符（位置编号从0开始）。超出返回`undefined`

### base64 转码

> 所谓 Base64 就是一种编码方法，可以将任意值转成 0～9、A～Z、a-z、`+`和`/`这64个字符组成的可打印字符。使用它的主要目的，不是为了加密，而是为了不出现特殊字符，简化程序的处理。

JavaScript 原生提供两个 Base64 相关的方法。

- `btoa()`：任意值转为 Base64 编码
- `atob()`：Base64 编码转为原来的值

> 注意，这两个方法不适合非 ASCII 码的字符，会报错。

```js
btoa('你好') // 报错
```

要将非 ASCII 码字符转为 Base64 编码，必须中间插入一个转码环节，再使用这两个方法。

```js
function b64Encode(str) {
  return btoa(encodeURIComponent(str));
}

function b64Decode(str) {
  return decodeURIComponent(atob(str));
}

b64Encode('你好') // "JUU0JUJEJUEwJUU1JUE1JUJE"
b64Decode('JUU0JUJEJUEwJUU1JUE1JUJE') // "你好"
```

## 对象

> 什么是对象？简单说，对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。

- 对象的属性之间用逗号分隔, 最后一个属性后面可加可不加.

- 对象的属性值如果引用的是对象,则是不同对象的属性引用同一个对象,是同一块内存地址,改一个,影响另一个,

- 如果引用是原始类型的值, 则是值的拷贝, 互不影响

- 行首是大括号开头的 是表达式还是语句?

  ```js
  { foo: 123 }
  ```

  - 为了避免歧义, V8引擎规定, 如果行首是大括号, 一律解释为对象. 为了避免歧义, 最好在大括号前加上圆括号.

  - 这种差异在`eval`语句(作用是对字符串求值) 中体现明显: 

    ```js
    eval('{foo: 123}') // 123
    eval('({foo: 123})') // {foo: 123}
    ```

    上面代码中, 如果没有圆括号, `eval`将其理解为代码块, 加上括号后理解成一个对象.

- **属性的读取**

  - 读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符。

  - 使用方括号运算符，键名必须放在引号里面，否则会被当作变量处理。

    - 方括号例外: 数字键可以不加引号, 因为会自动转化为字符串
    - 数值键名不能使用点运算符（因为会被当成小数点），只能使用方括号运算符。

  - JavaScript 允许属性的“后绑定”，也就是说，你可以在任意时刻新增属性，没必要在定义对象的时候，就定义好属性。

  - 查看一个对象的所有属性, 用 `Object.keys`

  - 属性的删除用 `delete`, 成功删除返回 `true` 在没有被删除属性时也会返回 `true`   

  - ```js
    `delete object.name  // true`		
    ```

  - `delete`只有一种情况会返回 `false` : 属性存在, 但不得删除

  - `delete`命令只能删除对象本身的属性，无法删除继承的属性

- 用 `in`查看属性是否从存在 (键名)  `'name' in object`

  - 继承的也会返回 `true`
  - 这时，可以使用对象的`hasOwnProperty`方法判断一下，是否为对象自身的属性。

- 属性的遍历 `for in`

  ```js
  for (var i in obj) {
    console.log('键名：', i);
    console.log('键值：', obj[i]);
  }
  ```

  - 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。
  - 它不仅遍历对象自身的属性，还遍历继承的属性(必须是可遍历的)。



- **with**操作同一个对象的多个属性时，提供一些书写的方便。

## 函数

> 函数是一段可以反复调用的代码块

### 函数声明

有三种

- function命令
- 函数表达式
- Function构造函数
