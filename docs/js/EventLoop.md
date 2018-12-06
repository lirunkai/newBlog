# EventLoop

说到EventLoop就要说下js是单线程的，为了实现主进程不堵塞， 才有了EventLoop这种解决方案

**同步任务**

优先执行的

**异步任务**

**宏任务**(macroTask)

`setTimeout` `setInterval` `setImmediate` `I/O` `UI rendering`

**微任务**(microTask)

`Promise.then` `process.nextTick`

同步任务优先执行, 之后会执行异步任务, 异步任务分为宏任务和微任务。 微任务会在宏任务之前执行

也就是 `同步任务 微任务 宏任务` 重复

| 注意:
|
| 在每一次事件循环中，macrotask 只会提取一个执行，而 microtask 会一直提取，直到 microtasks 队列清空

```
console.log(1);

setTimeout(function() {
  console.log(8);
}, 2);

setTimeout(function() {
  console.log(6);
}, 1);

setTimeout(function() {
  console.log(7);
}, 0);



new Promise((re, rj) => {
  console.log(2)
  re(3)
})
.then(function() {
  console.log(4);
}).then(function() {
  console.log(5);
});

console.log(3);
// 12345678
```
