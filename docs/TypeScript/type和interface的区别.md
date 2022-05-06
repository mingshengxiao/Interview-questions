**type**: 类型别名，使用 type 创建类型别名，类型别名不仅可以用来表示基本类型，还可以用来表示对象类型、联合类型、元组和交集。

**interface**: 接口，接口是命名数据结构（例如对象）的另一种方式；与 type 不同，interface 仅限于描述对象类型。

### type 和 interface 的相同点

1. 都可以描述 Object 和 Function

```js
// type

type Point = {
  x: number,
  y: number,
};

type SetPoint = (x: number, y: number) => void;

// interface

interface Point {
  x: number;
  y: number;
}

interface SetPoint {
  (x: number, y: number): void;
}
```

2. 都可以被继承

> 类型别名能通过交叉类型运算符&扩展 interface 或者任意有效的 Typescript 类型

```js
type Person = {
  name: string,
};

interface Student extends Person {
  age: number;
}

type Woman = Person & { walk: () => void };

type S2 = Student & { book: string };

interface Man extends Student {
  run: () => void;
}
```

3. 都可以实现 implements

类可以实现 interface 以及 type(除联合类型外)

```js
interface ICat {
  setName(name: string): void;
}

class Cat implements ICat {
  setName(name: string): void {
    // todo
  }
}

// type
type ICat = {
  setName(name: string): void,
};

class Cat implements ICat {
  setName(name: string): void {
    // todo
  }
}
```

### type 和 interface 的区别

1. 类型别名可以为任何类型引入名称。例如基本类型，联合类型，元祖类型等
2. 类型别名不支持继承，类型别名不能通过继承定义，但可以通过交叉类型运算符&扩展 interface 或者任意有效的 Typescript 类型
3. 类型别名不会创建一个真正的名字
4. 类型别名重名时编译器会抛出错误，接口重名时会产生合并
