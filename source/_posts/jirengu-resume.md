---
title: 会动的简历
date: 2018-04-08 15:29:28
tags: [JavaScript, es6, vue]
categories: Front-End
---

#会动的简历

> 总结收获

## ##知识点

- 使用的是String.substring()的方法实现一定时间增加一个字符渲染到div中
- 这里用的是VUE的数据做到同步更新
- Promise的用法：
  使用的是 async function(){
      await 接 Promise对象
  }
- Vue中无法直接添加style可以用div包含着把style标签放进去使之生效；

## ##插件

1.[markedjs](https://github.com/markedjs/marked)
把markdown语法的字段转为html代码字段

>   项目中用法：
>   `marked(xxx)`
> xxx:md文本 转化为html语句
>
> 2.[prismjs](https://prismjs.com/)
> 把需要高亮的代码加上类名
>   项目中用法：
>   `Prism.highlight(this.code, Prism.languages.css)`
> this.coded是要高亮的语句
> Prims.languages.css使用高亮的方法变量

