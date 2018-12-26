---
title: classList-原生代替jquery的类名切换属性
date: 2018-10-15 09:47:44
tags: JavaScript
categories: Front-End
---

 ## MDN描述

`Element.classList` 是一个只读属性,返回元素的类属性的实时`DOMTokenList`集合.

使用`classList`是代替`element.className`作为空格分隔的字符串访问元素的类列表的一种简便方法.

### 语法

> let elementClasses = elementNodeReference.classList;

**elementClasses**是一个`DOMTokenList`表示`elementNodeReference`的类属性.如果元素为设置类名则属性为空. 则 **elementClasses.length**返回0. 虽然 **element.classList**本身是只读的,但是可以使用 **add()**和 **remove()**方法修改它.

## 方法

**add( String [, String] )**

​	添加指定的类值. 如果类存在 则忽略.可以是多个

**remove( String [,String] )**

​	删除指定的类值. 可以是多个.

**item ( Number )**

​	按集合中的索引返回类值.

**toggle( String [, force] )** 

​	当只有一个参数时, 切换类值.

​	当有第二个参数时, 如果第二个参数计算结果为ture,则添加指定类值.如果为false.则删除它.

**contains( String )**

​	检查元素的了类属性中是否存在指定的类值

**replace( oldClass, newClass )**
​	用一个新类替换已有的类.



### 兼容性

chrome和firefox支持所有属性.

ie10 只实现处理一个参数,**add/remove方法不支持多参数处理**。默认只会处理第一个参数

opera和safari除了`replace`未实现,其他都已实现.

