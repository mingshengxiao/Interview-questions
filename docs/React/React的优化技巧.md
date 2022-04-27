1. 使用纯组件

如果 React 组件为相同的状态和 props 渲染相同的输出，则可以将其视为纯组件。

**PureComponent 的浅层比较**: 在对比先前的 props 和状态与下一个 props 和状态时，浅层比较将检查它们的基元是否有相同的值（例如：1 等于 1 或真等于真），还会检查更复杂的 JavaScript 值（如对象和数组）之间的引用是否相同。

2. 使用 React.memo 进行组件记忆

React.memo 是一个高阶组件。它会记忆上次某个输入 prop 的执行输出并提升应用性能。即使在这些组件中比较也是浅层的。

3. 使用 shouldComponentUpdate 生命周期事件

这是在重新渲染组件之前触发的其中一个生命周期事件。

可以利用此事件来决定何时需要重新渲染组件。如果组件 props 更改或调用 setState，则此函数返回一个 Boolean 值。

```js
import React from "react";

export default class ShouldComponentUpdateUsage extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: "test",
      age: 30,
      mark: "1",
    };
  }

  componentDidMount() {
    setTimeout(() => {
      this.setState({
        mark: "2",
      });
    });
  }

  shouldComponentUpdate(nextPRops, nextState) {
    if (
      nextState.age !== this.state.age ||
      nextState.name !== this.state.name
    ) {
      return true;
    }
    return false;
  }

  render() {
    return (
      <div>
        <b>User Name:</b> {this.state.name}
        <b>User Age:</b> {this.state.age}
      </div>
    );
  }
}
```

从 shouldComponentUpdate 传递 true 就意味着可以重新渲染组件，反之亦然。所以正确使用 shouldComponentUpdate 就可以优化应用组件的性能。

4. 懒加载组件

**Suspense 和 lazy**

```js
import React, { lazy, Suspense } from "react";

export default class CallingLazyComponents extends React.Component {
  render() {
    var ComponentToLazyLoad = null;

    if (this.props.name == "Mayank") {
      ComponentToLazyLoad = lazy(() => import("./mayankComponent"));
    } else if (this.props.name == "Anshul") {
      ComponentToLazyLoad = lazy(() => import("./anshulComponent"));
    }
    return (
      <div>
        <h1>This is the Base User: {this.state.name}</h1>
        <Suspense fallback={<div>Loading...</div>}>
          <ComponentToLazyLoad />
        </Suspense>
      </div>
    );
  }
}
```

5. 使用 React.Fragments 避免额外标记
6. 不要使用内联函数定义

如果我们使用内联函数，则每次调用“render”函数时都会创建一个新的函数实例。

当 React 进行虚拟 DOM diffing 时，它每次都会找到一个新的函数实例；因此在渲染阶段它会会绑定新函数并将旧实例扔给垃圾回收。

因此直接绑定内联函数就需要额外做垃圾回收和绑定到 DOM 的新函数的工作。

```js
import React from "react";

export default class InlineFunctionComponent extends React.Component {
  setNewStateData = (event) => {
    this.setState({
      inputValue: e.target.value,
    });
  };

  render() {
    return (
      <div>
        <h1>Welcome Guest</h1>
        <input
          type="button"
          onClick={this.setNewStateData}
          value="Click For Inline Function"
        />
      </div>
    );
  }
}
```

7. 避免 componentWillMount()中的异步请求
8. 在 constructor 的早期绑定函数

当我们在 React 中创建函数时，我们需要使用 bind 关键字将函数绑定到当前上下文。最好在构造函数调用期间使用绑定到当前上下文的函数覆盖 handleButtonClick 函数。

这将减少将函数绑定到当前上下文的开销，无需在每次渲染时重新创建函数，从而提高应用的性能。

9. 箭头函数与构造函数中的绑定

当我们添加箭头函数时，该函数被添加为对象实例，而不是类的原型属性。这意味着如果我们多次复用组件，那么在组件外创建的每个对象中都会有这些函数的多个实例。

每个组件都会有这些函数的一份实例，影响了可复用性。此外因为它是对象属性而不是原型属性，所以这些函数在继承链中不可用。

10. 避免使用内联样式属性
11. 优化 React 中的条件渲染

安装和卸载 React

12. 不要在 render 方法中导出数据
13. 为组件创建错误边界
14. 组件的不可变数据结构

React 的灵魂是函数式编程。如果我们希望组件能一致工作，则 React 组件中的状态和 props 数据应该是不可变的。

15. 使用唯一键迭代

渲染项目列表时应该为项目添加一个键。

16. 事件节流和防抖
17. 使用 CDN
18. 用 CSS 动画代替 JavaScript 动画
19. 在 Web 服务器上启用 gzip 压缩
20. 使用 Web Workers 处理 CPU 密集任务
21. React 组件的服务端渲染
