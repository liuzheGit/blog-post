---
title: mvc思想
date: 2018-10-26 16:43:16
tags: [mvc,JavaScript]
categories: Front-End
---

## 起源

2010年, Backbone.js出现.



## 单词

- increase 加
- decrease 减
- square 平方
- cube 立方

## 意大利面条

> 思想是: 用动态页面,: 获取数据 > 更新数据 > 更改数据 > 更新数据.



## 一些程序员想出了解决办法

**一些程序员通过自己的总结，发现这些代码总是可以分成三类：**

1. 专门操作远程数据的代码（fetchDb 和 saveDb 等等）
2. 专门呈现页面元素的代码（innerHTML 等等）
3. 其他控制逻辑的代码（点击某按钮之后做啥的代码）

**为什么分成这三类呢？因为我们前端抄袭了后端的分类思想，后端代码也经常分为三类：**

1. 专门操作 MySQL 数据库的代码
2. 专门渲染 HTML 的代码
3. 其他控制逻辑的代码（用户请求首页之后去读数据库，然后渲染 HTML 作为响应等等）

**这些思路经过慢慢的演化，最终被广大程序员完善为 MVC 思想。**

1. M 专门负责数据
2. V 专门负责表现
3. C 负责其他逻辑

**如果我们来反思一下，会发现这个分类是无懈可击的：**

1. 每个网页都有数据
2. 每个网页都有表现（具体为 HTML）
3. 每个网页都有其他逻辑

## 未改造前[例子1](https://jsbin.com/noraye/8/edit?html,js,output)

## 第一次MVC改造 [例子2](https://jsbin.com/yuwopuf/3/edit?js,output)

就分为三部分

1. 控制数据库数据的获取和更新,需要一个data对象来本地存储

2. ```js
   let model = {
     data: {
       id: null,
       name: '',
       number: 0
     },
     fetch(id) {
       return axios.get(`/books/${id}`).then((response)=>{
         this.data = response.data;
       })
     },
     update(newData){
       let id = this.data.id
       return axios.put(`/books/${id}`,newData).then((response)=>{
         this.data= response.data;
       })
     }
     
   }
   ```

2. 把操作页面显示的分离出来

3. ```js
   let view = {
     el: "#app",
     template: `
     <div>
       书名：《__name__》，
       数量：<span id="number">__number__</span>
     </div>
     <div class="actions">
       <button id="increaseByOne">加1</button>
       <button id="decreaseByOne">减1</button>
       <button id="square">平方</button>
       <button id="cube">立方</button>
       <button id="reset">归零</button>
     </div>
     `,
     render(data){
       $(this.el).html(
         this.template.replace('__number__', data.number)
           .replace('__name__', data.name)
       )
     }
   }
   ```

3. 控制器 主要 运用 把事件用数据化的思维进行绑定, 把更新数据分离成一个`updateModel` 方法, 绑定事件用到了bind绑定当前的conteroller作用域,而不是window

4. ```js
   var controller = {
     init({view, model}){
       this.view = view;
       this.model = model;
       this.view.render(this.model.data);
       this.bindEvents();
       this.fetchModel();
     },
     events: [
       { type: 'click', selector: '#increaseByOne', fnName: 'add'},
       { type: 'click', selector: '#decreaseByOne', fnName: 'minus'},
       { type: 'click', selector: '#square', fnName: 'square'},
       { type: 'click', selector: '#cube', fnName: 'cube'},
       { type: 'click', selector: '#reset', fnName: 'reset'},
     ],
     bindEvents(){
       this.events.map((event)=>{
         $(this.view.el).on(event.type, event.selector, this[event.fnName].bind(this))
       })
     },
     add(){
       let newData = {number: this.model.data.number + 1};
       this.updateModel(newData)
     },
     minus(){
       let newData = {number: this.model.data.number - 1};
       this.updateModel(newData)
     },
     square(){
       let newData = {number: Math.pow(this.model.data.number, 2)};
       this.updateModel(newData)
     },
     cube(){
       let newData = {number: Math.pow(this.model.data.number, 3)};
       this.updateModel(newData)
     },
     reset(){
       let newData = {number: 0};
       this.updateModel(newData)
     },
     updateModel(newData){
       this.model.update(newData).then(()=>{
             console.log(this.model.data)
         this.view.render(this.model.data)
       })
     },
     fetchModel(){
       this.model.fetch(1).then(() =>{
         this.view.render(this.model.data)
       })
     }
   }
   
   controller.init({view, model})
   ```

4. 最后 把mvc 调用一下

5. ```
   controller.init({view, model})
   ```

5. 前置代码(后台)

6. ```js
   // 用到axios ajax库, 和 jquery来操作dom
   axios.interceptors.response.use(function (response) {
     let {config: {url, method, data}} = response
     data = JSON.parse(data||'{}')
     let row = {
       id: 1, name: 'JavaScript高级程序设计', number: 2
     }
     if(url === '/books/1' && method === 'get'){
       response.data = row
     }else if(url === '/books/1' && method === 'put'){
       response.data = Object.assign(row, data)
     }
     return response
   })
   ```

## 面向对象

一个页面或模块只需要 model view controller 三个对象
第二个页面就需要再来 model2 view2 controller2 三个对象
第三个页面就需要再来 model3 view3 controller3 三个对象
……
第N个页面就需要再来 modelN viewN controllerN 三个对象

你每次写一个 model 都要写很类似的代码
你每次写一个 view 都要写很类似的代码
你每次写一个 controller 都要写很类似的代码

为什么不利用模板代码（俗称面向对象）把重复的代码写到一个类呢（JS里面就是把「共有属性」放到原型里）

[代码](https://jsbin.com/sodojac/5/edit?js,output)

**理解**

- Model中的data参数有时不需要{},有时需要
- View 中 `for in`的用法
- array的map方法是有返回值的forEach.
- vue这个框架 data中的数据提升可. 例如: vue.name === vue.data.name;
