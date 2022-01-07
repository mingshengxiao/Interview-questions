#### React 生命周期有哪些，16 版本生命周期发生了哪些变化？

**React16 版本前和 16 版本后的生命周期有所不同，重点要清楚 React16 版本的改动**

React 的周期分为初始化阶段、挂载阶段、更新阶段和卸载阶段。

React15 版本:

初始化阶段:

**constructor**: 构造函数  
**getDefaultProps**: 获取 props 的默认值  
**getDefaultState**: 获取 STate 的默认值

挂载阶段:

**componentWillMount**: 组件初始化渲染前调用  
**render**: 组件渲染阶段  
**componentDidMount**: 组件挂载到 DOM 后调用

更新阶段:

**componentWillReceiveProps**: 组件将要接收新 props 前调用  
**shouldComponentUpdate**: 组件是否需要更新  
**componentWillUpdate**: 组件更新前调用  
**render**: 组件更新渲染阶段  
**componentDidUpdate**: 组件更新后调用

卸载阶段:

**componentWillUnMount**: 组件卸载前调用

**16 版本相比之前的版本多了一个错误处理**

React16 版本:

初始化阶段:

**constructor**: 构造函数  
**getDefaultProps**: 获取 props 的默认值  
**getDefaultState**: 获取 STate 的默认值

挂载阶段:

**static getDerivedStateFromProps(props, state)**: 组件每次被 rerender 的时候，包括在组件构建之后(虚拟 dom 之后，实际 dom 挂载之前)，每次获取新的 props 或 state 之后；每次接收新的 props 之后都会返回一个对象作为新的 state，返回 null 则说明不需要更新 state  
**render**: 组件渲染阶段
**componentDidMount**: 组件挂载到 DOM 后调用

更新阶段:

**static getDerivedStateFromProps(props,state)**:  
**shouldComponentUpdate**: 组件是否需要更新  
**render**: 组件更新渲染阶段  
**getSnapshotBeforeUpdate(prevProps,prevState)**: 触发时间: update 发生的时候，在 render 之后，在组件 dom 渲染之前；返回一个值，作为 componentDidUpdate 的第三个参数  
**componentDidUpdate**: 组件更新后调用

卸载阶段:

**componentWillUnMount**: 组件卸载前调用

错误处理:

**componentDidCatch**: 错误处理

#### react16 为什么要去掉 15 的那些生命周期
