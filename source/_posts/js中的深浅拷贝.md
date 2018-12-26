---
title: js中的深浅拷贝
date: 2018-09-08 15:30:04
tags: JavaScript
categories: Front-End
---
- 先贴代码

## 浅拷贝

```js
	function shallowCopy(oldObj) {
	    var newObj = {};
	    for(var i in oldObj) {
	        if(oldObj.hasOwnProperty(i)) {
	            newObj[i] = oldObj[i];
	        }
	    }
	    return newObj;
	}
```

## 深拷贝

```js
	function deepCopy(oldObj) {
        var newObj = {};
        for(var key in oldObj) {
            if(typeof oldObj[key] === 'object') {
                newObj[key] = deepCopy(oldObj[key]);
            }else{
                newObj[key] = oldObj[key];
            }
        }
        return newObj;
    }

```

# 总结一下

- 首先深拷贝和浅拷贝只针对Object、Array这样的复杂对象。简单来说，浅拷贝只会将各个属性进行复制，不会进行递归复制，而JavaSript储存对象都是存的地址，所以浅拷贝中如果有子对象。就会和拷贝的那个 指向同一内存地址。而深拷贝则会开辟新的内存地址，从而不会因为一个的改变影响到另一个。