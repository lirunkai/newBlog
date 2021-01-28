Vue-router

原理

HTML5 提供了 History API 来实现 URL 的变化。其中做最主要的 API 有以下两个：history.pushState() 和 history.repalceState()。这两个 API 可以在不进行刷新的情况下，操作浏览器的历史纪录。唯一不同的是，前者是新增一个历史记录，后者是直接替换当前的历史记录

+ pushState 和 repalceState 两个 API 来操作实现 URL 的变化 
+ 我们可以使用 popstate 事件来监听 url 的变化。只有在做出浏览器动作时，才会触发该事件，如用户点击浏览器的回退按钮（或者在Javascript代码中调用`history.back()`或者`history.forward()`方法）
+ history.pushState() 或 history.replaceState() 不会触发 popstate 事件，这时我们需要手动触发页面跳转（渲染）

安装

`yarn add vue-router@4`

使用

```javascript
const routes = [
	{ path: '/', component: Home},
	{ path: '/about', component: About}
]

const router = VueRouter.createRouter({
	history: VueRouter.createWebHasHistory(),
	routes
})

const app = Vue.createApp({})
app.use(router)
```

