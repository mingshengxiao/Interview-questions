### 实现一个 JSON.stringify

<b>JSON.stringify()</b> 方法将一个 JavaScript 对象或值转换为 JSON 字符串，如果指定了一个 replacer 函数，则可以选择性地替换值，或者指定的 replacer 是数组，则可选择性地仅包含数组指定的属性。

JSON.stringify(value[,replacer[,space]])：

replacer: 如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为 null 或者未提供，则对象所有的属性都会被序列化。

space: 指定缩进用的空白字符串，用于美化输出（pretty-print）；如果参数是个数字，它代表有多少的空格；上限为 10。该值若小于 1，则意味着没有空格；如果该参数为字符串（当字符串长度超过 10 个字母，取其前 10 个字母），该字符串将被作为空格；如果该参数没有提供（或者为 null），将没有空格。

- 当尝试去转换 BigInt 类型的值会抛出 TypeError ("BigInt value can't be serialized in JSON")（BigInt 值不能 JSON 序列化）.
- 对包含循环引用的对象（对象之间相互引用，形成无限循环）执行此方法，会抛出错误。

- Boolean|Number|String 类型会自动转换成对应的原始值。
- undefined、任意函数以及 symbol，会被忽略（出现在非数组对象的属性值中时），或者被转换成 null（出现在数组中时）。
- 非数组对象的属性不能保证以特定的顺序出现在序列化后的字符串中。
- 不可枚举的属性会被忽略
- 属性值 Infinity,-Infinity,undefined,NaN 经过 stringify 转换后会变成 null
- 所有以 symbol 为属性键的属性都会被完全忽略掉，即便 replacer 参数中强制指定包含了它们。
- 其他类型的对象，包括 Map/Set/WeakMap/WeakSet，仅会序列化可枚举的属性。

### 代码实现

<p>递归实现</p>

```js
function jsonStringify(obj) {
  let type = typeof obj;
  if (type !== "object" || type === null) {
    if (/function|undefined|symbol/.test(type)) {
      return undefined;
    }
    if (/string/.test(type)) {
      obj = '"' + obj + '"';
    }
    return String(obj);
  }

  let json = [];
  const isArray = obj && obj.constructor === Array;

  for (let k in obj) {
    let v = obj[k];
    let type = typeof v;
    // undefined、任意函数以及 symbol，会被忽略（出现在非数组对象的属性值中时）
    // 当在数组对象中时，应该返回null
    if (/function|undefined|symbol/.test(type)) {
      continue;
    } else if (/string/.test(type)) {
      v = '"' + v + '"';
    } else if (type === "object") {
      v = jsonStringify(v);
    }
    json.push((isArray ? "" : '"' + k + '":') + String(v));
  }

  return (isArray ? "[" : "{") + String(json) + (isArray ? "]" : "}");
}
```

```js
function jsonStringify(data) {
  let dataType = typeof data;

  if (dataType !== "object") {
    let result = data;
    //data 可能是 string/number/null/undefined/boolean
    if (Number.isNaN(data) || data === Infinity) {
      //NaN 和 Infinity 序列化返回 "null"
      result = "null";
    } else if (
      dataType === "function" ||
      dataType === "undefined" ||
      dataType === "symbol"
    ) {
      //function 、undefined 、symbol 序列化返回 undefined
      return undefined;
    } else if (dataType === "string") {
      result = '"' + data + '"';
    }
    //boolean 返回 String()
    return String(result);
  } else if (dataType === "object") {
    if (data === null) {
      return "null";
    } else if (data.toJSON && typeof data.toJSON === "function") {
      return jsonStringify(data.toJSON());
    } else if (data instanceof Array) {
      let result = [];
      //如果是数组
      //toJSON 方法可以存在于原型链中
      data.forEach((item, index) => {
        if (
          typeof item === "undefined" ||
          typeof item === "function" ||
          typeof item === "symbol"
        ) {
          result[index] = "null";
        } else {
          result[index] = jsonStringify(item);
        }
      });
      result = "[" + result + "]";
      return result.replace(/'/g, '"');
    } else {
      //普通对象
      /**
       * 循环引用抛错(暂未检测，循环引用时，堆栈溢出)
       * symbol key 忽略
       * undefined、函数、symbol 为属性值，被忽略
       */
      let result = [];
      Object.keys(data).forEach((item, index) => {
        if (typeof item !== "symbol") {
          //key 如果是symbol对象，忽略
          if (
            data[item] !== undefined &&
            typeof data[item] !== "function" &&
            typeof data[item] !== "symbol"
          ) {
            //键值如果是 undefined、函数、symbol 为属性值，忽略
            result.push('"' + item + '"' + ":" + jsonStringify(data[item]));
          }
        }
      });
      return ("{" + result + "}").replace(/'/g, '"');
    }
  }
}
```

##### 实现 JSON.parse

<p>直接使用eval存在XSS攻击，需要对输入内容进行检验</p>
<p>通过new Function()实现<strong>此方法待验证</strong></p>
<code>
  var jsonStr = '{"age": 20, "name": "jack}';
  var json = (new Function('return ' + jsonStr))();
</code>
