## EventLoop

说到EventLoop就要说下js是单线程的，为了实现主进程不堵塞， 才有了EventLoop这种解决方案

**同步任务**

优先执行的

同步任务都在主线程执行， 会形成一个调用栈

**异步任务**

**宏任务**(macroTask / task)

`setTimeout` `setInterval` `setImmediate` `I/O` `UI rendering`

**微任务**(microTask / jobs)

`Promise.then` `process.nextTick`

同步任务优先执行, 之后会执行异步任务, 异步任务分为宏任务和微任务。 微任务会在宏任务之前执行

也就是 `同步任务 微任务 宏任务` 重复

> 注意:
>
> 在每一次事件循环中，macrotask 只会提取一个执行，而 microtask 会一直提取，直到 microtasks 队列清空

```javascript
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

> setTimeout的延迟执行时间不得小于1ms, 如果小于1ms, 设置为1毫秒
>
> ```c++
> repeat *= 1; // coalesce to number or NaN
> 	  if (!(repeat >= 1 && repeat <= TIMEOUT_MAX))
> 		repeat = 1; // schedule on next tick, follows browser behavior
> 	
> 	  var timer = new Timeout(repeat, callback, args);
> 	  timer._repeat = repeat;
> 	  if (process.domain)
> 		timer.domain = process.domain;
> 	
> 	  active(timer);
> 	
> 	  return timer;
> ```

#### vue的nextTick也是利用微任务来实现的。



### 事件机制

事件传播的三个阶段 **捕获 ** **冒泡** **抵达当前触发事件的元素**

捕获： body -> 元素父级 -> 目标元素

冒泡:  目标元素 -> 元素父级 -> body

#### 事件的注册

`target.addEventListener(eventType, listener, [options])`

`options`

1. `options.capture`  表示 `listener` 会在该类型的事件捕获阶段传播到该 `EventTarget` 时触发。
2. `options.once` 表示`listener`在添加之后最多调用一次
3. `options.passive` 表示 `listener` 永远不会调用 `preventDefault()。`

`target.addEventListener(eventType, listener, [useCapture])`

`useCapture`决定了事件的传播方式`  true时, 父级优先于子集元素接受事件.

#### 取消事件的监听

`removeEventListener(eventType, listener)`

#### 事件派发

`target.dispatchEvent(event)` 

+ event 是要被派发的事件对象
+ target 被用来初始化事件和决定将会触发目标

### 事件对象

`e` 在事件处理函数内部，您可能会看到一个固定指定名称的参数, 如 `e`被称为事件对象

`e.target` 事件刚刚发生的元素的引用

### 阻止事件的默认行为

`event.preventDefault()`  有些按钮上有一些浏览器注册的特性, 比如`input(type="submit")` 会进行表单的提交, 通过`event.preventDefault()`可以阻止这一默认行为.

#### 取消冒泡

`event.stopPropagation()`  取消冒泡，只会让当前事件处理程序运行，但事件不会在**冒泡**链上进一步扩大，

### 事件委托

冒泡还允许我们利用事件委托

如果你想要在大量子元素中单击任何一个都可以运行一段代码，您可以将事件监听器设置在其父节点上，并让子节点上发生的事件冒泡到父节点上，而不是每个子节点单独设置事件监听器

优点:

1. 减少内存消耗
2. 新增节点时, 不需要单独添加事件

#### 事件是怎么实现的？



---

### 面试

1. js为什么是单线程的？

因为js可以修改DOM结构，如果js引擎线程不是单线程那么就可以执行多段js，如果多段js都操作DOM，就会造成DOM冲突

为了避免DOM渲染冲突, js采用了单线程.

单线程的问题： 如果任务队列里有一个任务耗时长，就会导致这个任务后的任务一直排队等待，发生页面卡死，影响用户体验。

为了解决这个问题： js将任务的执行分为同步和异步, 异步再细分为宏任务和微任务， 执行顺序分别为 同步任务->微任务->宏任务

2. 怎么判断页面是否加载完成?

   Load事件表示页面中的DOM，CSS， JS图片全部已经加载完毕

   DOMContentLoaded表示初始的HTML完全加载和解析