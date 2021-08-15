- script 标签中 async 跟 defer 的区别

设置async和defer的目的都是不阻塞浏览器解析其他文档。

**defer**

被设置为defer的脚本，浏览器会立即下载，但是会延迟到整个页面都解析完毕后再运行。

HTML5规范要求脚本按照它们出现的先后顺序执行，因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于DOMContentLoaded事件执行。在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在DOMContentLoad时间触发前执行，因此最好只包含一个延迟脚本

**async**

被设置为async的脚本，浏览器一旦加载完成会立即执行。

具体的区别如下图:

![async和defer](../assets/images/async和defer.png)

