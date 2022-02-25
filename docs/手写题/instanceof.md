### 作用

用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。

```js
// 定义构造函数
function C() {}
function D() {}

var o = new C();

o instanceof C; // true，因为 Object.getPrototypeOf(o) === C.prototype

o instanceof D; // false，因为 D.prototype 不在 o 的原型链上

o instanceof Object; // true，因为 Object.prototype.isPrototypeOf(o) 返回 true
C.prototype instanceof Object; // true，同上

C.prototype = {};
var o2 = new C();

o2 instanceof C; // true

o instanceof C; // false，C.prototype 指向了一个空对象,这个空对象不在 o 的原型链上.

D.prototype = new C(); // 继承
var o3 = new D();
o3 instanceof D; // true
o3 instanceof C; // true 因为 C.prototype 现在在 o3 的原型链上
```

> 需要注意的是，如果表达式 obj instanceof Foo 返回 true，则并不意味着该表达式会永远返回 true，因为 Foo.prototype 属性的值有可能会改变，改变之后的值很有可能不存在于 obj 的原型链上，这时原表达式的值就会成为 false。另外一种情况下，原表达式的值也会改变，就是改变对象 obj 的原型链的情况，虽然在目前的 ES 规范中，我们只能读取对象的原型而不能改变它，但借助于非标准的 \_\_proto\_\_ 伪属性，是可以实现的。比如执行 obj.**\_\_proto\_\_** = {} 之后，obj instanceof Foo 就会返回 false 了。

### 原理

instanceof 在查找的过程中会遍历左边变量的原型链，直到找到右边变量的原型对象，返回 true，否则查找失败，返回 false

### 手写

```js
// instanceof
function myInstanceOf(instance, target) {
  if (typeof instance !== "object" || instance === null) {
    return false;
  }
  let left = Object.getPrototypeOf(instance);
  while (left) {
    if (left === target.prototype) {
      return true;
    }
    left = Object.getPrototypeOf(left);
  }
  return false;
}
```
