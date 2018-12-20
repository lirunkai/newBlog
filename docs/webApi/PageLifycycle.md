# PageLifecycle

网页的生命周期， 通过这个API我们可以更自如的去控制网页的运行

分为6个阶段, 任何时刻只能是其中一个阶段

**Active**

网页处于可见状态,且拥有输入焦点。 拥有`focus`事件

**Passive**

网页可见, 但没有输入焦点, 无法输入。 拥有`blur`事件

**Hidden**

网页不可见, 但是尚未冻结. UI不再更新, 用户离开当前网页

**Terminated**

用户主动关闭窗口，或者在同一个窗口前往其他页面，导致当前页面开始被浏览器卸载并从内存中清除

**Frozen**

长时间不操作, 进入Frozen状态   

**Discarded**

长时间处于Frozen状态, 用户不唤醒页面的话就会进入Discarded状态 浏览器会自动卸载网页，清除内存的占用.

## visibilitychange

`visibilitychange`事件在网页的可见状态发生改变时触发.

`document.onvisibilitychange`

`document.visibilityState`的值

 1. `visible` 页面部分可见, 没有最小化

 2. `hidden` 用户不可见

 3. `prerender` 正在渲染

 4. `unloaded` 页面从内存中卸载清除

```
// 获取Active Passive Hidden的状态
docuemnt.visibilityState === hidden    //Hidden
document.hasFocus()  === true  // Active
other     // Passive
```

## resume

`resume`事件： 网页离开`Frozen`阶段，进入`/Active/Passive/Hidden`阶段时触发

`document.onresume = function（){}`

## beforeunload

窗口或文档即将卸载时触发， 经过这个事件, 网页进入`Frozen`阶段

## freeze

在网页进入`Frozen`阶段时触发

`document.onfreeze = function（){}`

## unload

页面正在卸载时触发, 经过这个事件, 网页进入`Discarded`状态

`document.wasDiscarded` 如果页面被丢弃过, 返回true

## pageshow

`pageshow` 在用户加载网页时触发. 加载网页分为 全新的页面加载或者从缓存中获取的页面, `event.persisted`为`true`.否则就是`false`

跟浏览器的`History`记录的变化有关

## pagehide

`pagehide` 用户离开当前网页、进入另一个网页时触发

跟浏览器的`History`记录的变化有关


---

引用

[PageLifecycle 阮一峰教程](http://www.ruanyifeng.com/blog/2018/11/page_lifecycle_api.html)
