## jsx

描述当前组件内容的数据结构

JSX在运行时的返回结果（即React.createElement()的返回值）都是React Element

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

### useState

`let [x, setX] = useState()`

1. 不能写在判断条件中

### useEffect

```javascript
useEffect(() => {
  // 卸载
  return () => {}
}, [依赖])
```

### React.memo

对比前后两次props是否有修改, 有修改进行重新渲染

### useMemo

第一个参数为函数, 函数的返回值是useMemo的返回值,

第二个参数是数组, 当数组项发生变化时, useMemo重新计算


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