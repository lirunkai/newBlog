# Proxy

拦截， 代理。 拦截住了就代理上, 没拦截就通过

`new Proxy(target, handler)`

## 可拦截的

拦截**属性**的读取  `handler.get(target, propKey)`

拦截**属性**的设置, 返回一个布尔值  `handler.set(target, propKey, value)`

拦截**in**操作， 返回一个布尔值 `handler.has(target,propKey)`

拦截**delete**操作, 返回一个布尔值 `handler.deleteProperty(target, propKey)`

拦截**getOwnPropertyDescriptor**操作,返回属性的描述对象。 `handler.getOwnPropertyDescriptor(target, propKey)`

拦截**defineProperty**操作 `handler.defineProperty(target, propKey, propDesc)`


## 拦截后

当拦截到我们想拦截的, 我们可以对他们的默认行为进行修改。

```
eg:
// 确保内部属性不会被修改

let handler = {
  set(target, propKey, value){
    if(propKey[0] == '_'){
      return new Error(`can not set ${propKey}`)
    }
    target[propKey] = value
    return true;
  }
}

let obj = {a: 1, _a: 2}

let proxy = new Proxy(obj, handler)

proxy._a = 2
```
