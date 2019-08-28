## Vue和React的区别

### 数据响应

Vue: Vue的数据响应是通过`Object.defineProperty`自动响应数据的变化, 更新数据.

React：react是函数式的思想，把组件设计成纯组件，状态和逻辑通过参数传入，所以在react中，是单向数据流，推崇结合immutable来实现数据不可变。react在setState之后会重新走渲染的流程，如果shouldComponentUpdate返回的是true，就继续渲染，如果返回了false，就不会重新渲染



### 模板

Vue使用的是单文件

React使用的是`jsx` 


### 数据检测

React： 我们通常会用`setState`API显式更新,然后React会进行 Virtual Dom Diff操作找出差异,然后Patch到DOM上,React从一开始就不知道到底是哪发生了变化,只是知道「有变化了」,然后再进行比较暴力的Diff操作查找「哪发生变化了」，另外一个代表就是Angular的脏检查操作

Vue：Vue初始化时对数据data进行依赖的收集，当数据发生变化时，响应式系统立马会得知哪里发生变化，触发watcher进行更新。但是每个data的每个key都有一个watcher，watcher过多会造成内存增高，所以Vue在组件级别通过第一时间侦测到发生变化的组件,然后在组件内部进行Virtual Dom Diff获取更加具体的差异


### 全局组件

Vue, 有全局组件的概念. 声明了之后在任何组件都可以使用

React 使用任何组件都是需要先声明再使用.
