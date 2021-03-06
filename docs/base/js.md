js

引入: 通过script标签

+  async 异步加载, 执行时会阻塞元素渲染
+  defer：延迟加载，元素解析完成后加载

类

#### new干了什么？

+ 创建了一个对象
+ 对象有个`__proto__`属性， 指向类的原型
+  修改this的指向
+  如果构造函数返回的是对象， 则返回这个对象

实现

```javascript
function myNew(fn, ...args) {
  let obj = {}
	obj.__proto__ = fn.prototype
  let result = fn.call(obj, ...args)
  if(typeof result === 'object' || typeof result === 'function') {
    return result
  } else {
    return obj
  }
}
```



#### 原型

每个函数都会创建一个prototype的属性，这个属性是一个对象,包含实例共享的属性和方法。

每个实例上都有一个`__proto__`属性, 指向创建函数的原型`prototype`

#### 原型链

原型链是主要的继承方式。原型链指的是实例在继承父类时, 实例的原型是父类的实例

`实例.__proto__= 原形.prototype`

主要思想就是原型是另一个类型的实例。也就是这个原型本身有一个内部指针(`__proto__`)指向另一个原型, 相应的另一个原型也有一个指针指向另一个构造函数。这样就在实例和原形之间构造了一条原型链

#### Instanceof原理？

不断找原型

```javascript

```



#### 执行上下文

变量或函数的上下文决定了它们可以访问哪些数据，以及它们的行为。 每个上下文都有一个关联对象，这个上下文中定义的所有变量和函数都存在于这个对象上。无法通过代码访问，但是在后台处理数据时会用到

+ 全局作用域
+ 块级作用域
+ (特殊作用域)闭包

#### 作用域链

作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到 `window`对象即被终止，作用域链向下访问变量是不被允许的

#### 闭包

闭包是函数和声明该函数的词法环境的组合

闭包的一大特性就是**内部函数总是可以访问其所在的外部函数中声明的参数和变量，即使在其外部函数被返回（寿命终结）了之后**

#### this的指向？

+ 普通函数`this`是动态的，指向调用者。 可通过`call apply`修改指向
+ 箭头函数的`this`是在定义时确定了的。 无法修改



#### Promise 异步

js是单进程的。

##### 为什么是单进程的？

思考一个场景， 如果是多进程的，那么多个进程同时修改dom，以哪个进程为主？

##### 单进程会有什么问题？

当读取一个文件特别大时， 会阻塞后面程序的运行。怎么解决呢？ 异步`EventLoop`

##### 事件循环`EventLoop`

先执行宏任务队列，再执行微任务队列。然后开启下一轮事件循环。

+ 宏任务: setTimeout/setInterval/I/O/UI Rending/scripts
+ 微任务: process.nextTick()/Promise.then

##### Promise



##### proxy可以拦截哪些操作

`get` `set` `deleteProperty` 

`has` in操作

 `ownKeys`  for....in等循环操作

`apply` 拦截proxy实例作为函数调用的操作

`constructor` 拦截proxy实例作为构造函数调用的操作

`setPrototype` 拦截`Object.setPrototype`，返回一个boolean

`getPrototypeOf(target)`：拦截`Object.getPrototypeOf(proxy)`，返回一个对象

##### Reflect

在proxy内部调用对象的默认行为。



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



EventLoop

js主线程在运行时会产生执行栈, 栈中的代码调用某些异步API时会在任务队列中添加事件,栈中的代码执行完毕后，会读取任务队列中的事件，去执行事件对应的回调函数, 如此循环往复, 形成事件循环机制

js中有两种任务类型, 微任务和宏任务。 微任务会优先于宏任务执行

宏任务: `setTimeout setInterval setImmediate I/O`

微任务: `Promise.then Object.observe MutationObserver process.nextTick`

nodejs中的宏任务分成了几种类型, 并且放在了不同的`task queue`里。微任务放在了每个`task queue`的末尾

1. `setTimeout/setInterval` 属于timer类型
2. `incoming, connections,data,etc` 属于`poll`回调
3. `setImmediate` 属性check类型
4. `socket`的`close`属于`close callback`类型



模块

+ 一个复杂的程序依据一定的规则封装成几个块，并进行组合在一起
+ 快的内部数据与实现是私有的, 只是向外部暴露一些接口来实现通信

好处:

+ 避免命名冲突
+ 更好的分离， 按需加载
+ 更高的复用性，可维护性

规范

`ES Module`

`exports` / `import`

`CommonJs`

`module.exports`/ `require`

区别：

+ **CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用**
+ **CommonJS 模块是运行时加载，ES6 模块是编译时输出接口**。



##### `isNaN` 和 `Number.isNaN`的区别

`isNaN`会先将参数转为数值，不能转为数字的返回true

`Number.isNaN`会首先判断传入参数是否为数字，如果是数字再继续判断是否为NaN