- webpack中bundle，chunk，module的作用

bundle 是由Webpack打包出来的文件;

chunk 代码块,一个chunk由多个模块组合⽽成，⽤于代码的合并和分割;

module 是开发中的单个模块，在Webpack中⼀个模块对应⼀个⽂件，Webpack会从配置的entry中递归开始找出所有依赖的模块。

- Loader和Plugin的区别

Loader直译为"加载器"。Webpack将⼀切⽂件视为模块，但是Webpack原⽣是只能解析JavaScript⽂件，如果想将其他⽂件也打包的话，就会⽤到Loader。所以Loader的作⽤是让Webpack拥有了加载和解析非JavaScript文件的能力;

Plugin直译为"插件"。Plugin可以扩展Webpack的功能,让Webpack具有灵活性。在Webpack运⾏的⽣命周期中会⼴播出许多事件，Plugin可以监听这些事件，在合适的时机通过Webpack提供的API改变输出结果。

- module.exports和exports的区别

exports是module.exports的一个引用

- es module 和 commonjs 的区别

commonjs只能在运行时确定导出的接口，实际导出的就是一个对象。esModule是在编译时运行的。因此import具有提升效果，会提升到整个模块的头部，首先执行。

commonjs中require的是被导出的值的拷贝，即一旦导出这个值，模块内部的变化就影响不到这个值。commonjs在第一次导入模块后将该模块缓存，在后续再导入该模块时，会直接从缓存中获取。

```js
// a.js
var name = 'morrain'
var age = 18
exports.name = name
exports.age = age
exports.setAge = function(a){
    age = a
}
// b.js
var a = require('a.js')
console.log(a.age) // 18
a.setAge(19)
console.log(a.age) // 18
```

import导入的是值的引用。

```js
// a.js
var name = 'morrain'
var age = 18
const setAge = a => age = a
export {
    name,
    age,
    setAge
}
 
// b.js
import * as a from 'a.js'
 
console.log(a.age) // 18
a.setAge(19)
console.log(a.age) // 19
```
