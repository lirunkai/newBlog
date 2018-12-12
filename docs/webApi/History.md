# History

允许操作浏览器的访问历史。。。

history对象保存了当前窗口访问过的所有页面网址.

## 方法

`history.back()` 回退到上一个页面

`history.forward()` 移动到下一个网址

`history.go()`  以当前网址为基准, 移动到对应的网址， 负数向上, 正数向下

`history.pushState(state, title, url)`

| state 一个与添加的记录相关联的状态对象，主要用于popstate事件。该事件触发时，该对象会传入回调函数。也就是说，浏览器会将这个对象序列化以后保留在本地，重新载入这个页面的时候，可以拿到这个对象。如果不需要这个对象，此处可以填null

在历史中添加一条记录, 浏览器的url展示为新的url， 但是不会跳转到新的url, 也就是说 `pushState()`不会触发页面刷新.

`history.replaceState(state, title, url)` 修改history的当前记录

## 属性

`history.state` 可以拿到`pushState`的state对象

`history.length` 当前窗口访问过的网址数量

## 事件

`popstate`

每当同一个文档的浏览历史（即history对象）出现变化时，就会触发popstate事件。

只有用户点击浏览器倒退按钮和前进按钮，或者使用 `history.go()  history.forward() history.back()`方法时才会触发。

`pushState() replaceState()` 不会触发
