- 使用setTimeout模拟setInterval的原因

setInterval只是在指定的间隔时间将任务添加到任务队列中，何时执行该任务则是根据任务队列中的任务执行情况而定的。

setInterval的缺点:

1. 使用setInterval时，某些间隔会被跳过
2. 可能多个定时器会连续执行

每个setTimeout产生的任务会直接push到任务队列中，而setInterval会在每次把任务push到任务队列前，都要进行一下判断(看上次的任务是否仍在队列中，如果有则不添加，没有则添加).

```js
let n = customSetTimeout(func, interval) {
  setTimeout(function() {
    func();
    n(func, interval);
  }, interval);
}
```