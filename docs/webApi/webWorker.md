# web worker

## Service Worker

Service workers 本质上充当的角色是Web应用程序与浏览器之间的代理服务器, 也可以在网络可用时作为浏览器的网络间的代理.

| 运行在https协议上. 不能访问DOM. 完全异步, 同步API不能在servie worker中使用

采用JS控制关联的页面或者网站, 拦截并修改访问和资源请求，细粒度地缓存资源.

在后台持续运行.....

### 注册

`navigator.serviceWorker.register()` 返回一个promise

```
if('serviceWorker' in navigator){
  navigator.serviceWorker.register('./worker.js')     //worker.js的位置是打包之后的相对位置
  .then(() => console.log('load server worker'))
  .catch(err => console.error('some wrong:', error))
}

```

### 生命周期

 1. 下载

 2. 安装

 3. 激活

 用户首次访问service worker控制的网站时, service worker会立刻被下载. 之后每24小时会下载一次.

`install` 准备service worker用于使用触发, 安装完成

`activate` 主要用途是清理先前版本的service worker 脚本中使用的资源

`message`

`fetch`

`sync`

`push`
