### ES6

- let/const
- Promise
- Class
- 扩展操作符
- 箭头函数
- 函数参数默认值
- 模板字符串
- BigInt
- Map/WeakMap
- Set/WeakSet
- 迭代器/生成器
- 模块化(EsModule)

```js
// 模块 A 导出一个方法
export const sub = (a, b) => a + b;
// 模块 B 导入使用
import { sub } from "./A";
console.log(sub(1, 2)); // 3
```

- for...of
- Symbol
- Proxy/Reflect
- 对象属性简写
- 解构赋值

### ES7

- Array.prototype.includes()
- 求幂运算符(2 \*\* 4)

### ES8

- Async/Await

Async/await 让你的代码看起来是同步的，在某种程度上，也使得它的行为更加地同步。 await 关键字会阻塞其后的代码，直到 promise 完成，就像执行同步操作一样。它确实可以允许其他任务在此期间继续运行，但您自己的代码被阻塞。

这意味着您的代码可能会因为大量 await 的 promises 相继发生而变慢。每个 await 都会等待前一个完成，而你实际想要的是所有的这些 promises 同时开始处理（就像我们没有使用 async/await 时那样）。

- Object.entries()、Object.values()
- Object.getOwnPropertyDescriptors()

用来获取一个对象的所有自身属性的描述符。

```js
const obj = {
  name: "jimmy",
  age: 18,
};
const desc = Object.getOwnPropertyDescriptors(obj);
console.log(desc);
// 打印结果
{
  name: {
    value: 'jimmy',
    writable: true,
    enumerable: true,
    configurable: true
  },
  age: {
   value: 18,
   writable: true,
   enumerable: true,
   configurable: true
  }
}
```

- String.prototype.padStart

把指定字符串填充到字符串头部，返回新字符串。

```js
str.padStart(targetLength [, padString])
```

```js
const now = new Date();
const year = now.getFullYear();
// 月份和日期 如果是一位前面给它填充一个0
const month = (now.getMonth() + 1).toString().padStart(2, "0");
const day = now.getDate().toString().padStart(2, "0");
console.log(year, month, day);
console.log(`${year}-${month}-${day}`); //输入今天的日期 2021-12-31
```

- String.prototype.padEnd

把指定字符串填充到字符串尾部，返回新字符串。

- 尾逗号 Trailing commas
- SharedArrayBuffer 对象

> SharedArrayBuffer 对象用来表示一个通用的，固定长度的原始二进制数据缓冲区

- Atomics 对象

> Atomics 对象提供了一组静态方法用来对 SharedArrayBuffer 对象进行原子操作

### ES9

- Object Rest & Spread

```js
const input = {
  a: 1,
  b: 2,
  c: 3,
};

const output = {
  ...input,
  c: 4,
};

console.log(output); // {a: 1, b: 2, c: 4}
```

- for await of

异步迭代器(for-await-of)：循环等待每个 Promise 对象变为 resolved 状态才进入下一步。

```js
function TimeOut(time) {
  return new Promise(function (resolve, reject) {
    setTimeout(function () {
      resolve(time);
    }, time);
  });
}

async function test() {
  let arr = [TimeOut(2000), TimeOut(1000), TimeOut(3000)];
  for await (let item of arr) {
    console.log(Date.now(), item);
  }
}
test();
// 1560092345730 2000
// 1560092345730 1000
// 1560092346336 3000
```

- Promise.prototype.finally()

Promise.prototype.finally() 方法返回一个 Promise，在 promise 执行结束时，无论结果是 fulfilled 或者是 rejected，在执行 then()和 catch()后，都会执行 finally 指定的回调函数。这为指定执行完 promise 后，无论结果是 fulfilled 还是 rejected 都需要执行的代码提供了一种方式，避免同样的语句需要在 then()和 catch()中各写一次的情况。

- String 扩展

### ES10(ES2019)

- Object.fromEntries()

方法 Object.fromEntries() 把键值对列表转换为一个对象，这个方法是和 Object.entries() 相对的。

```js
Object.fromEntries([
  ["foo", 1],
  ["bar", 2],
]);
// {foo: 1, bar: 2}

// Map转Object
const map = new Map();
map.set("name", "jimmy");
map.set("age", 18);
console.log(map); // {'name' => 'jimmy', 'age' => 18}

const obj = Object.fromEntries(map);
console.log(obj);
// {name: "jimmy", age: 18}

// 过滤对象中符合条件的属性
// course表示所有课程，想请求课程分数大于80的课程组成的对象：
const course = {
  math: 80,
  english: 85,
  chinese: 90,
};
const res = Object.entries(course).filter(([key, val]) => val > 80);
console.log(res); // [ [ 'english', 85 ], [ 'chinese', 90 ] ]
console.log(Object.fromEntries(res)); // { english: 85, chinese: 90 }

// url的search参数转换
// let url = "https://www.baidu.com?name=jimmy&age=18&height=1.88"
// queryString 为 window.location.search
const queryString = "?name=jimmy&age=18&height=1.88";
const queryParams = new URLSearchParams(queryString);
const paramObj = Object.fromEntries(queryParams);
console.log(paramObj); // { name: 'jimmy', age: '18', height: '1.88' }
```

- Array.prototype.flat()

```js
let newArray = arr.flat([depth]);
```

- Array.prototype.flatMap()

flatMap() 方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。从方法的名字上也可以看出来它包含两部分功能一个是 map，一个是 flat（深度为 1）。

```js
var new_array = arr.flatMap(function callback(currentValue[, index[, array]]) {
    // 返回新数组的元素
}[, thisArg])
```

- String.prototype.trimStart()
- String.prototype.trimEnd()
- 可选的 Catch Binding

```js
try {
  console.log("Foobar");
} catch {
  console.error("Bar");
}
```

- Symbol.prototype.description

> 只读属性，返回 Symbol 对象的可选描述的字符串。

- JSON.stringify() 增强能力
- 修订 Function.prototype.toString()

以前函数的 toString 方法来自 Object.prototype.toString(),现在的 Function.prototype.toString() 方法返回一个表示当前函数源代码的字符串。以前只会返回这个函数，不包含注释、空格等。

```js
function foo() {
  // es10新特性
  console.log("imooc");
}
console.log(foo.toString());
// 打印如下
// function foo() {
//  // es10新特性
//  console.log("imooc");
// }
```

### ES11(Es2020)

- 空值合并运算符（Nullish coalescing Operator）

空值合并操作符（ ?? ）是一个逻辑操作符，当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数。

- 可选链 Optional chaining

> 可选链不能用于赋值

- globalThis

现在 globalThis 提供了一个标准的方式来获取不同环境下的全局 this 对象（也就是全局对象自身）。不像 window 或者 self 这些属性，它确保可以在有无窗口的各种环境下正常工作。所以，你可以安心的使用 globalThis，不必担心它的运行环境。

- BigInt

BigInt 不能用于 [Math] 对象中的方法；不能和任何 [Number] 实例混合运算，两者必须转换成同一种类型。在两种类型来回转换时要小心，因为 BigInt 变量在转换成 [Number] 变量时可能会丢失精度。

- String.prototype.matchAll()

matchAll() 方法返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器。

```js
const regexp = /t(e)(st(\d?))/g;
const str = "test1test2";

const array = [...str.matchAll(regexp)];
console.log(array[0]); // ["test1", "e", "st1", "1"]
console.log(array[1]); // ["test2", "e", "st2", "2"]
```

- Promise.allSettled()

- Dynamic Import（按需 import）

import()可以在需要的时候，再加载某个模块。

```js
button.addEventListener("click", (event) => {
  import("./dialogBox.js")
    .then((dialogBox) => {
      dialogBox.open();
    })
    .catch((error) => {
      /* Error handling */
    });
});
```

### ES12(ES2021)

- 逻辑运算符和赋值表达式（&&=，||=，??=）
- String.prototype.replaceAll()
- 数字分隔符

ES2021 中允许 JavaScript 的数值使用下划线（\_）作为分隔符。

- Promise.any

方法接受一组 Promise 实例作为参数，包装成一个新的 Promise 实例返回。

Promise.any()跟 Promise.race()方法很像，只有一点不同，就是 Promise.any()不会因为某个 Promise 变成 rejected 状态而结束，必须等到所有参数 Promise 变成 rejected 状态才会结束。

```js
const promise1 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise1");
      //  reject("error promise1 ");
    }, 3000);
  });
};
const promise2 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise2");
      // reject("error promise2 ");
    }, 1000);
  });
};
const promise3 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise3");
      // reject("error promise3 ");
    }, 2000);
  });
};
Promise.any([promise1(), promise2(), promise3()])
  .then((first) => {
    // 只要有一个请求成功 就会返回第一个请求成功的
    console.log(first); // 会返回promise2
  })
  .catch((error) => {
    // 所有三个全部请求失败 才会来到这里
    console.log("error", error);
  });
```

- WeakRef and Finalizers

> 使用 WeakRefs 的 Class 类创建对对象的弱引用(对对象的弱引用是指当该对象应该被 GC 回收时不会阻止 GC 的回收行为)
