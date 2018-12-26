---
title: JavaScript基础复习5-属性描述对象
date: 2018-11-05 16:42:01
tags: JavaScript
categories: Front-End
---

- 如果属性已经存在，`Object.defineProperty()`方法相当于更新该属性的属性描述对象。

- 如果一次性定义或修改多个属性，可以使用`Object.defineProperties()`方法。

- 注意，一旦定义了取值函数`get`（或存值函数`set`），就不能将`writable`属性设为`true`，或者同时定义`value`属性，否则会报错。

- `Object.defineProperty()`和`Object.defineProperties()`参数里面的属性描述对象，`writable`、`configurable`、`enumerable`这三个属性的默认值都为`false`。

- 对于`writeable`为`false`的 在严格模式下,修改值报错,但是普通模式不报错,会默认失效.

- 如果原型对象的某个属性的`writable`为`false`，那么子对象将无法自定义这个属性。

- ```js
  var proto = Object.defineProperty({}, 'foo', {
    value: 'a',
    writable: false
  });
  
  var obj = Object.create(proto);
  
  obj.foo = 'b';
  obj.foo // 'a'
  ```

- 但是，有一个规避方法，就是通过覆盖属性描述对象，绕过这个限制。原因是这种情况下，原型链会被完全忽视。

## 元属性

属性描述对象的各个属性称为“元属性”，因为它们可以看作是控制属性的属性。

## enumberable

如果一个属性的`enumerable`为`false`，下面三个操作不会取到该属性。

- `for..in`循环
- `Object.keys`方法
- `JSON.stringify`方法

`JSON.stringify`方法会排除`enumerable`为`false`的属性，有时可以利用这一点。如果对象的 JSON 格式输出要排除某些属性，就可以把这些属性的`enumerable`设为`false`。

## 对象的拷贝

有时，我们需要将一个对象的所有属性，拷贝到另一个对象，可以用下面的方法实现。

```js
var extend = function (to, from) {
  for (var property in from) {
    to[property] = from[property];
  }

  return to;
}

extend({}, {
  a: 1
})
// {a: 1}
```

上面这个方法的问题在于，如果遇到存取器定义的属性，会只拷贝值。

```
extend({}, {
  get a() { return 1 }
})
// {a: 1}
```

为了解决这个问题，我们可以通过`Object.defineProperty`方法来拷贝属性。

```js
var extend = function (to, from) {
  for (var property in from) {
    if (!from.hasOwnProperty(property)) continue;
    Object.defineProperty(
      to,
      property,
      Object.getOwnPropertyDescriptor(from, property)
    );
  }

  return to;
}

extend({}, { get a(){ return 1 } })
// { get a(){ return 1 } })
```

上面代码中，`hasOwnProperty`那一行用来过滤掉继承的属性，否则会报错，因为`Object.getOwnPropertyDescriptor`读不到继承属性的属性描述对象。
