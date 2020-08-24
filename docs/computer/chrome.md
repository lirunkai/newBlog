这里说一些浏览器的事情.

### CSSOM

1. 提供给js操作样式表的能力
2. 为布局树的合成提供基础的样式信息

DOM和CSSOM通常是并行构建的， CSSOM不会阻塞DOM的解析

由于Render Tree是依赖DOM Tree和CSSOM Tree的， 所以必须等到两者都加载完成后， 完成相应的构建，才开始渲染，所以CSS加载会阻塞DOM的渲染

### 渲染引擎

GUI 渲染线程与 JavaScript 引擎为互斥

当 JavaScript 引擎执行时 GUI 线程会被挂起,GUI 更新会被保存在一个队列中等到引擎线程空闲时立即被执行。

当浏览器在执行 JavaScript 程序的时候,GUI 渲染线程会被保存在一个队列中,直到 JS 程序执行完成,才会接着执行。

因此如果 JS 执行的时间过长,这样就会造成页面的渲染不连贯,导致页面渲染加载阻塞的感觉。

### 异步加载js

defer： js加载完成后, 整个文档解析后触发DOMContentLoaded事件前执行， **defer会等待HTML文档解析完成**

async： js加载完成后，浏览器空闲时，load事件触发前执行  **async脚本什么时候加载完， 什么时候执行， 会影响HTML的解析**

两者都是异步去加载js文件， 不会阻塞DOM解析

DOMContentloaded: DOM解析完成后触发，不包括样式表，图片等资源

load： 页面上所有的DOM，样式表，脚本，图片等资源加载完毕触发

