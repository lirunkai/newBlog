# window

主要说下window上挂载的一些API

`window.navigator.onLine` true有网, false没网

`window.addEventListener('online', (e) => { })` 监听浏览器的联网状态， 有网了触发

`window.addEventListener('offline', (e) => {})` 监听浏览器的联网状态, 没网了触发

`navigator.vibrate(time)` 震动多久
