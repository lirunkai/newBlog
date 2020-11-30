## jsx

描述当前组件内容的数据结构

JSX在运行时的返回结果（即React.createElement()的返回值）都是React Element

jsx会被babel解析为`React.createElement(type, config, children)`

在`createElement`函数中对参数进行标准化

---
1. 为什么每个jsx文件中都必须显示声明React?

因为`jsx`会被`@babel/plugin-transform-react-jsx`解析，

解析时会被解析成`React.createElement`，如果没有显示声明React，在模块运行时该模块内会报**未定义变量React**的错误

2. 为什么需要key?

需要通过key来查询两棵树是否有同一节点

+ 在两个树对比过程中, 如果没有key, 节点交换位置的时候会直接销毁这两个节点， 而不是复用

3. react的Diff算法？

完全diff的话很慢。

react对diff做了3层限制:

  1. 只对同级Diff
  2. 两个不同类型的元素会产生不同的树
  3. 开发者可以通过 key prop来暗示哪些子元素在不同的渲染下能保持稳定


4. requestIdleCallback

requestIdleCallback回调的执行前提条件是当前浏览器处于空闲状态

```javascript
requestIdleCallback(myNonEssentialWork)

function myNonEssentialWork(deadline) {
  // deadline.timeRemaining() 可以获取到当前帧的剩余时间
  while(deadline.timeRemaining() > 0 && tasks.length > 0) {
    doWorkIfNeeded()
  }

  if(tasks.length > 0) {
    requestIdleCallback(myNonEssentialWork)
  }
}
```

react为什么要自己实现requestIdleCallback？

页面的流畅度要求是60，而requestIdleCallback的FPS只有20, 远远低于了页面流畅度的要求， 所以react需要自己实现requestIdleCallback

react中requestIdleCallback的实现.

1. 非dom环境, 通过setTimeout来模拟

```javascript
requestIdleCallback = (callback) => {
  setTimeout(callbaclk({
    timeRemaining() {
      return Infinity
    }
  }))
}
```

2. 浏览器环境下

```javascript
let frame
let n = 5
function callback(timeStamp) {
  console.log(timeStamp)
  while(n > 0) {
    requestAnimationFrame(callback)
    console.log('测试执行顺序')
    n--
  }
}

frame = requestAnimationFrame(callback)
// 如果想销毁该回调
cancelAnimationFrame(frame)
```

## Hooks

一套能够使函数组件更强大, 更灵活的钩子

为什么需要Hooks？

1. 函数组件更贴合react的设计思想`UI=render(data)`
2. 函数组件真正的把数据和渲染绑定到了一起
3. 函数组件与类组件相比, 缺失了一些零件， 通过hooks来实现这些零件



hooks的底层依赖于顺序链表

### useState

`let [x, setX] = useState()`

setX 可接收一个值或者一个函数， 接收函数时, 参数为上一次的值， 接收值时, 将x设置为当前值

1. 不能写在判断条件中

2. 写多个useState还是写一个useState根据业务的力度

  + 将完全不相关的 state 拆分为多组 state,比如 size 和 position
  + 如果某些 state 是相互关联的，或者需要一起发生改变，就可以把它们合并为一组 state。比如 left 和 top。

### useEffect

```javascript
useEffect(() => {
  // 卸载
  return () => {}
}, [依赖])
```

### useCallback


### React.memo

包裹整个组件。 

避免重新渲染: 对比前后两次props是否有修改, 有修改进行重新渲染

### useMemo

第一个参数为函数, 函数的返回值是useMemo的返回值,

第二个参数是数组, 当数组项发生变化时, useMemo重新计算

适用的场景

1. 成本很高的计算。 有些计算开销很大，我们就需要「记住」它的返回值，避免每次 render 都去重新计算

2. 保持引用相等。 由于值的引用发生变化，导致下游组件重新渲染，我们也需要「记住」这个值

不适合的场景

1. 返回的值是原始值
2. 仅在组件内部用到的 object、array、函数等（没有作为 props 传递给子组件），且没有用到其他 Hook 的依赖数组中，一般不需要使用 useMemo

### useRef()

返回一个有带有 `current` 可变属性的普通对象.


[React Hooks正确使用](https://zhuanlan.zhihu.com/p/85969406)

---

1. 虚拟DOM和真实DOM的区别?

真实DOM操作代价高,  虚拟DOM操作非常简单

真实DOM消耗的内存比较大, 虚拟DOM消耗内存很小

2. 什么是react？

+ 用于构建用户界面的 JavaScript 库
+ 声明式编写 UI，可以让你的代码更加可靠，且方便调试

3. react的特点

+ 使用虚拟DOM, 而不是真正的DOM
+ 可以用服务器进行渲染
+ 遵循单向数据流
+ 提高了应用的性能
+ JSX， 代码的可读性更好

4. 虚拟DOM的工作原理

+ 每当底层数据发生变化时, 整个UI都将在虚拟DOM描述中重新渲染
+ 然后计算之前DOM标示与新标示之间的差异
+ 完成计算后, 将只用实际更改的内容更新real DOM

5. 虚拟dom的优点？
   1. 研发体验好，效率快
   2. 跨平台
   3. 差量更新（在修改数据量小的情况下）,性能比较好

6. react和vue的区别

   1. 本质上的区别：react是构建UI的库，vue是渐进式的框架
   2. 渲染上的区别: react通过setState去手动渲染页面 vue通过依赖收集自动响应修改

   