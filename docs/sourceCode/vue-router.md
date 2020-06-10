## vue-router

##### 带着问题看源码

+ 如何不刷新进行更新？
+ 怎么实现嵌套路由表？
+ new VueRouter做了什么？
+ 路由守卫拦截怎么实现的？
+ 用了哪些设计模式？
+ `$router` 和 `$route`如何实时随url的修改变化?

`$router` 和 `$route`如何实时随url的修改变化?

```javascript
Vue.mixin({
  	//每次组件调用都会更新_routerRoot
    beforeCreate () {
      if (isDef(this.$options.router)) {
        this._routerRoot = this
        this._router = this.$options.router // _router是VueRouter的实例 可以调用VueRouter的方法
        this._router.init(this)
        // _route 会动态修改为_router.history.current
        Vue.util.defineReactive(this, '_route', this._router.history.current)
      } else {
        this._routerRoot = (this.$parent && this.$parent._routerRoot) || this
      }
      registerInstance(this, this)
    },
    destroyed () {
      registerInstance(this)
    }
  })
	// 绑定$router到Vue.prototype 实际的值是_routerRoot._router
  Object.defineProperty(Vue.prototype, '$router', {
    get () { return this._routerRoot._router }
  })
	// 绑定$route到Vue.prototype 实际的值是_routerRoot._route 
	// _route的值会随_router.history.current修改
  Object.defineProperty(Vue.prototype, '$route', {
    get () { return this._routerRoot._route }
  })
```

