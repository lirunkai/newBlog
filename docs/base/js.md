js

引入: 通过script标签

+  async 异步加载, 执行时会阻塞元素渲染
+  defer：延迟加载，元素解析完成后加载

类

new干了什么？

原型

Instanceof原理？

this的指向？

作用域

+ 全局作用域
+ 

+ (特殊作用域)闭包



模块化

es6: import/export

Commonjs: require/module.exports



函数



Number

`Number.isInteger(num)`  是否是整数 `Number.isInteger(1.00) //true`

`Number.isSafeInteger(num)` 是否在`Number.MIN_SAFE_INTEGER`和`Number.MAX_SAFE_INTEGER`之间

Math

`Math.min()` 最小数

`Math.max()` 最大数

`Math.ceil()` 始终向上舍入为最接近的整数

`Math.floor()` 始终向下舍入为最接近的整数

`Math.round()` 四舍五入

`Math.random()` 随机数



Array

创建

Array.from() 第一个参数是类数组对象.

栈方法

`push()` 推入

`pop()`  弹出

队列方法

`shift()` 从队首弹出

`push()`  推入到队尾

排序

`reverse()` 反向排列

`sort（）` 默认从小到大

+ `sort((a,b) => b-a)` 从大到小

迭代

`every()`

`some()`

`filter()`

`map()`

`forEach()`



Map

`let map = new Map()`

map和object不同的是

+ map的会维护键值对的插入顺序
+ map可以使用任意值为key

`get(get)`

`set(key, value)`

`has(key)`

`size()`

`delete(key)`

`clear()`



WeakMap 弱映射

`let wm = new WeakMap()`

弱映射的键只能是Object，或者继承自Object的类型

和Map相比没有clear() 和迭代方法



事件

事件流: 描述了页面接受事件的顺序，三个阶段 ： 事件捕获， 目标元素， 事件冒泡

事件冒泡：从最具体的元素开始触发, 然后向上传播至Document

事件捕获:  从Document节点向下捕获到具体的元素