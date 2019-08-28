## Vue和React的区别

### 数据响应

Vue的数据响应是通过`Object.defineProperty`自动响应数据的变化, 更新数据.

React需要通过`setState`来手动进行数据响应.



### 模板

Vue使用的是`template`模版

React使用的是`jsx` 



### 数据流

Vue是双向数据流

React是单向数据流



## 数据检测

React： 我们通常会用`setState`API显式更新,然后React会进行 Virtual Dom Diff操作找出差异,然后Patch到DOM上,React从一开始就不知道到底是哪发生了变化,只是知道「有变化了」,然后再进行比较暴力的Diff操作查找「哪发生变化了」，另外一个代表就是Angular的脏检查操作

Vue：Vue初始化时对数据data进行依赖的收集，当数据发生变化时，响应式系统立马会得知哪里发生变化，触发watcher进行更新。但是每个data的每个key都有一个watcher，watcher过多会造成内存增高，所以Vue在组件级别通过第一时间侦测到发生变化的组件,然后在组件内部进行Virtual Dom Diff获取更加具体的差异

