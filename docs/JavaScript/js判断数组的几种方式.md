### JS 判断数组的几种方式

1. 原型链

```js
obj.__proto__ === Array.prototype;
```

2. 通过 ES6 的 Array.isArray()判断

```js
Array.isArray(obj);
```

3. 通过 instanceof 判断

```js
obj instanceof Array;
```

4. 通过 Array.prototype.isPrototypeOf

```js
Array.prototype.isPrototypeOf(obj);
```

5. 通过 Object.prototype.toString.call()判断

```js
Object.prototype.toString.call(obj).slice(8, -1) === "Array";
```
