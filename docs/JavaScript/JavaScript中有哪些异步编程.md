- JavaScript中有哪些异步编程方式

1. 回调函数
```js
f1(f2);
```
优点: 易编写、易理解和易部署    
缺点: 不利于代码的阅读和维护，各个部分之间高度耦合

2. 事件监听
```js
f1.on('done', f2);
```
优点: 易理解，可以绑定多个事件，每个事件可以指定多个回调，有利于模块化    
缺点: 整个程序都变成事件驱动型，运行流程会变得不清晰

3. 发布/订阅
```js
f1: fn.publish('done');
f2: fn.subscribe('done', f2);
```

4. promise对象
```js
new Promise.resolve().then(f2)
```
Promises对象是CommonJS工作组提出的一种规范，目的是为异步编程提供统一接口；思想是，每一个异步任务返回一个Promise对象，该对象有一个then方法，允许指定回调函数。