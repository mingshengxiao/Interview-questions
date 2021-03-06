- script 标签中 async 跟 defer 的区别

JS 脚本的加载和执行会阻塞 DOM 的渲染，设置 async 和 defer 的目的都是不阻塞浏览器解析其他文档。

**defer**

被设置为 defer 的脚本，浏览器会立即下载，但是会延迟到整个页面都解析完毕后再运行。

HTML5 规范要求脚本按照它们出现的先后顺序执行，因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于 DOMContentLoaded 事件执行。在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoad 时间触发前执行，因此最好只包含一个延迟脚本

**async**

被设置为 async 的脚本，浏览器一旦加载完成会立即执行。

中文意思是异步，这个属性与 defer 类似，都用于改变处理脚本的行为。同样与 defer 类似，async 只适用于外部脚本文件，并告诉浏览器立即下载文件。但与 defer 不同的是，标记为 async 的脚本并不保证按照它们的先后顺序执行。

指定 async 属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容,这使用于之间互不依赖的各脚本。

具体的区别如下图:

![async和defer](../assets/images/async和defer.png)
