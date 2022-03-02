### FC

格式化上下文是决定盒子之间如何布局的环境，不同的格式化上下文如何布局盒子由自身的规则来决定。

块级盒（block-level Box）是描述元素跟它的父元素与兄弟元素之间的表现。

块容器盒（block container box）描述元素跟它的后代之间的影响。

### BFC 定义

BFC: 块级格式化上下文，是用于布局块级盒子的一块独立的渲染区域。让处于 BFC 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。

> BFC 是 Web 页面 CSS 视觉渲染的一部分，用于决定块盒子的布局及浮动相互影响范围的一个区域。 MDN - 块格式化上下文

> 具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。

- 触发 BFC 的方式:

1. 根元素，即 HTML 元素
2. 浮动元素，即 float 为 left、right
3. overflow 不是 visible，即值为 auto、scroll、hidden 的元素
4. display 值为 inline-block、table-cell、table-caption、table、inline-table、flex、inline-flex、grid、inline-grid、table-row、table-row-group、table-header-group、table-footer-group、flow-root
5. 定位元素: position 为 absolute、fixed
6. contain 为 layout、content、paint 的元素
7. 多列容器（元素的 column-count 或 column-width (en-US)不为 auto，包括 column-count 为 1）
8. column-span: all

- BFC 布局规则:

1. 浮动的元素会被父级计算高度(父级元素触发了 BFC),计算 BFC 的高度时，要考虑 BFC 所包含的所有子元素
2. 非浮动元素不会覆盖浮动元素的位置(非浮动元素触发了 BFC)
3. margin 不会传递给父级(父级触发 BFC)
4. 属于同一个 BFC 的两个相邻元素上下 margin 会重叠,不同 BFC 不会发生折叠
5. 内部盒子会在垂直方向排列
6. 当元素不是 BFC 的子元素时，浮动元素高度不参与 BFC 计算（常见的盒子塌陷问题）
7. 每个盒子（块盒与行盒）的 margin box 的左边，与包含块 border box 的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。

- 开发中应用:

1. 阻止 margin 重叠
2. 可以包含浮动元素 —— 清除内部浮动(清除浮动的原理是两个 div 都位于同一个 BFC 区域之中)
3. 自适应两栏布局
4. 可以阻止元素被浮动元素覆盖
5. 阻止因为浏览器因为四舍五入造成的多列布局换行的情况
6. 自适用两列布局（float + overflow）
7. 解决高度塌陷问题

> CSS2.1 中只有 BFC 和 IFC，CSS3 中才有 GFC 和 FFC。

### IFC(Inline Formatting Context):行级格式化上下文

**触发条件**: 块级元素中仅包含内联级别元素

当 IFC 中有块级元素插入时，会产生两个匿名块将父元素分割开来，产生两个 IFC。

- 布局规则

1. 在一个 IFC 内，子元素是水平方向横向排列的，并且垂直方向起点为元素顶部。
2. 子元素只会计算横向样式空间，【padding、border、margin】，垂直方向样式空间不会被计算，【padding、border、margin】。
3. 在垂直方向上，子元素会以不同形式来对齐（vertical-align）
4. 能把在一行上的框都完全包含进去的一个矩形区域，被称为该行的行框（line box）。行框的宽度是由包含块（containing box）和与其中的浮动来决定。
5. IFC 中的 line box 一般左右边贴紧其包含块，但 float 元素会优先排列。
6. IFC 中的 line box 高度由 CSS 行高计算规则来确定，同个 IFC 下的多个 line box 高度可能会不同。
7. 当 inline boxes 的总宽度少于包含它们的 line box 时，其水平渲染规则由 text-align 属性值来决定。
8. 当一个 inline box 超过父元素的宽度时，它会被分割成多个 boxes，这些 boxes 分布在多个 line box 中。如果子元素未设置强制换行的情况下，inline box 将不可被分割，将会溢出父元素。

- 应用场景

1. 元素水平居中

当一个块要在环境中水平居中时，设置其为 inline-block 则会在外层产生 IFC，通过 text-align 则可以使其水平居中。

2. 多行文本水平垂直居中

创建一个 IFC，然后设置其 vertical-align:middle，其他行内元素则可以在此父元素下垂直居中。

### GFC(Grid Formatting Contexts):栅格格式化上下文

触发方式:

```css
div {
  display: grid;
  // display: inline-grid;
}
```

### FFC(Flex Formatting Contexts):弹性格式化上下文

1. 设置为 flex 的容器被渲染为一个块级元素
2. 设置为 inline-flex 的容器被渲染为一个行内元素
3. 弹性容器中的每一个子元素都是一个弹性项目。弹性项目可以是任意数量的。弹性容器外和弹性项目内的一切元素都不受影响。简单地说，Flexbox 定义了弹性容器内弹性项目该如何布局

> FFC 布局中，float、clear、vertical-align 属性不会生效。
