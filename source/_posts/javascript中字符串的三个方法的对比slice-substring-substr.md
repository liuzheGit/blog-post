---
title: 'javascript中字符串的三个方法的对比slice,substring,substr'
date: 2018-6-10 21:41:59
tags: JavaScript
categories: Front-End
---

> slice，substring,substr三个函数都是截取字符串，但是对参数的处理有区别

**参数处理相似的两个函数式slice和substring**

slice(start,end)和substring(start,end)

他们两个的end都是原字符串的索引，意思为截取到end（不包括end）位置的字符

**二者的区别是：**

slice中的start如果为负数，会从尾部算起，-1表示倒数第一个，-2表示倒数第2个，此时end必须为负数，并且是大于start的负数，否则返回空字符串

slice的end如果为负数，同样从尾部算起，如果其绝对值超过原字符串长度或者为0，返回空字符串



substring会取start和end中较小的值为start,二者相等返回空字符串，任何一个参数为负数被替换为0(即该值会成为start参数)



**而substr比较特殊**

substr的end参数表示，要截取的长度,若该参数为负数或0，都将返回空字符串
