Vue-router

[传送门](https://router.vuejs.org/zh/)

安装

`yarn add vue-router`

使用

```
import VueRouter from 'vue-router'

Vue.use(VueRouter) 

// 敲黑板
let routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]
// 敲黑板
let  router = new VueRouter({
    routes,
    mode
})

new Vue(
    routes
)
```

### `在Vue.use(VueRouter)之后发生了什么？`

1. `$route`挂载到`Vue.prototype`上
2. `$router`挂载到`Vue.prorotype`上
3. 注册了全局组件`router-link`
4. 注册了全局组件`router-view`

`$route`上存储当前路由的信息

`$router`可以调用路由的方法

## mode

`history | hash | abstract`

## routes都有哪些定义好的属性

`path` 路径

`component` 组件

`children` 子集

`redirect` 重定向

`alias` 别名

`meta`  数据元信息

## 关于路由守卫

`beforeEach`

