# window

主要说下window上挂载的一些API

`window.navigator.onLine` true有网, false没网

`window.addEventListener('online', (e) => { })` 监听浏览器的联网状态， 有网了触发

`window.addEventListener('offline', (e) => {})` 监听浏览器的联网状态, 没网了触发

`navigator.vibrate(time)` 震动多久

`window.requestIdleCallback(callback, {timeout: 400ms})`    在浏览器空闲时期依次调用函数

 	1. cb， 接收一个`deadline`的参数, 拥有
      	1. timeRemaining  毫秒值
      	2. didTimeout， 如果是空闲时间调用返回false, 其他返回true

