# events

异步事件驱动. 基础包， 许多其他的包都会基于events来实现. `stream` `http` `fs` `process`等等

监听某个事件的触发, 然后执行监听器.

## 引入

`const EventEmitter = require('events')`

`const myEvent = new EventEmitter()` 必须实例后才可以使用

## 注册

`myEvent.on(eventName, handler)`

可多次注册同一eventName, 在eventName触发后， 所有注册的监听器`handler`都会触发

只处理一次的可以通过 `myEvent.once(eventName, handler)`来注册

```
const EventEmitter = require('events')

const myEvent = new EventEmitter();

myEvent.once('one', () => {
  console.log(1)
})

myEvent.once('one', () => {
  console.log(2)
})

myEvent.emit('one')

myEvent.emit('one')

// 1
// 2

```

*newListener* 注册后会触发`newListener`事件， 触发`handler(eventName, listener)`

*removeListener* 移除事件后, 触发`handler(eventName, listener)`

## 触发

`myEvent.emit(eventName)`

## 删除

`myEvent.off(eventName, handler)` 删除某个handler

`myEvent.removeListener(eventName, handler)` off的别名

`myEvent.removeAllListeners(eventName)` 删除所有监听器
