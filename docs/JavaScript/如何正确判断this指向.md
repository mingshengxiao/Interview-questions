### 如何正确判断 this 指向

一句话: 谁调用它，this 就指向谁

- 全局环境中的 this

浏览器环境：无论是否在严格模式下，在全局执行环境中（在任何函数体外部）this 都指向全局对象 window;

node 环境：无论是否在严格模式下，在全局执行环境中（在任何函数体外部），this 都是空对象 {};

- 是否是 new 绑定

1. 如果是 new 绑定，并且构造函数中没有返回 function 或者是 object，那么 this 指向这个新对象。
2. 构造函数返回值是 function 或 object， new Super()时返回的是 Super 中返回的对象。

```js
function Super(age) {
  this.age = age;
  let obj = { a: "2" };
  return obj;
}

let instance = new Super("hello");
console.log(instance); // {a: '2'}
console.log(instance.age); // undefined
```

3. 函数是否通过 call,apply 调用，或者使用了 bind 绑定，如果是，那么 this 绑定的就是指定的对象【归结为显式绑定】。

如果 call,apply 或者 bind 传入的第一个参数值是 undefined 或者 null，严格模式下 this 的值为传入的值 null /undefined。非严格模式下，实际应用的默认绑定规则，this 指向全局对象(node 环境为 global，浏览器环境为 window)

- 箭头函数的情况

箭头函数没有自己的 this，继承外层上下文绑定的 this。
