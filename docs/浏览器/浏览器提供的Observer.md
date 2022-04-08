### IntersectionObserver

IntersectionObserver 可以监听一个元素和可视区域相交部分的比例，然后在可视比例达到某个阈值的时候触发回调。

```js
const intersectionObserver = new IntersectionObserver(
  function (entries) {
    console.log("info:");
    entries.forEach((item) => {
      console.log(item.target, item.intersectionRatio);
    });
  },
  {
    threshold: [0.5, 1],
  }
);

intersectionObserver.observe(document.querySelector("#box1"));
intersectionObserver.observe(document.querySelector("#box2"));
```

做一些数据采集的时候，希望知道某个元素是否是可见的，什么时候可见的，就可以用这个 api 来监听，还有做图片的懒加载的时候，可以当可视比例达到某个比例再触发加载。

### MutationObserver

MutationObserver 可以监听对元素的属性的修改、对它的子节点的增删改。

```js
const mutationObserver = new MutationObserver((mutationsList) => {
  console.log(mutationsList);
});

mutationObserver.observe(box, {
  attributes: true,
  childList: true,
});
```

比如文章水印被人通过 devtools 去掉了，那么就可以通过 MutationObserver 监听这个变化，然后重新加上，让水印去不掉。

### PerformanceObserver

PerformanceObserver 用于监听记录 performance 数据的行为，一旦记录了就会触发回调，这样我们就可以在回调里把这些数据上报。

```js
<html>
  <body>
    <button onclick="measureClick()">Measure</button>

    <img
      src="https://p9-passport.byteacctimg.com/img/user-avatar/4e9e751e2b32fb8afbbf559a296ccbf2~300x300.image"
    />

    <script>
      const performanceObserver = new PerformanceObserver((list) => {
        list.getEntries().forEach((entry) => {
          console.log(entry); // 上报
        });
      });
      performanceObserver.observe({
        entryTypes: ["resource", "mark", "measure"],
      });

      performance.mark("registered-observer");

      function measureClick() {
        performance.measure("button clicked");
      }
    </script>
  </body>
</html>
```

### ResizeObserver

元素可以用 ResizeObserver 监听大小的改变，当 width、height 被修改时会触发回调。

```js
const resizeObserver = new ResizeObserver((entries) => {
  console.log("当前大小", entries);
});
resizeObserver.observe(box);
```

### ReportingObserver

ReportingObserver 可以监听过时的 api、浏览器干预等报告等的打印，在回调里上报，这些是错误监听无法监听到但对了解网页运行情况很有用的数据。
