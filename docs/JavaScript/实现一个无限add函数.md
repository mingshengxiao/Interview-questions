- 给定一个add函数，要支持以下形式的调用

Add(1)(2)(3).sumOf(); // 6
Add(1,2)(3)(4).sumOf() // 10
Add(1,2,...)(3)(4).sumOf() // ...

```js
  function Add(x) {
    const params = [ ...arguments];
    return function() {
      params.push(...arguments);
      return function() {
        params.push(...arguments);
        return params.reduce((a,b) => a + b);
      }
    }
  }

  console.log(Add(1)(2)(3));

  // 实现无限递归
  function Add() {
    const nums = [...arguments];
    function AddPro() {
      nums.push(...arguments);
      return AddPro;
    }

    AddPro.sumOf = () => {
      return nums.reduce((a,b) => a + b);
    }

    return AddPro;
  }

  // 写法二
  function sum(...args) {
    const f = (...rest) => {
      return sum(...[...args, ...rest]);
    }

    f.sumOf = () => {
      return args.reduce((x,y) =>  x + y, 0);
    }

    return f;
  }
```