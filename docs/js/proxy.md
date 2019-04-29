# Proxy

拦截， 代理。 拦截住了就代理上, 没拦截就通过

`new Proxy(target, handler)`

## 可拦截的

**get** 拦截属性的读取  `handler.get(target, propKey, receiver)`

**set** 拦截属性的设置, 返回一个布尔值  `handler.set(target, propKey, value, receiver)`

**apply** 拦截函数的调用, call和apply操作 `handler.apply(target, ctx, args)`

**has** 拦截HasProperty操作,比如`in Reflect.has()`， 返回一个布尔值 `handler.has(target,propKey)`

**construct** 拦截new操作, 返回的必须是一个对象，否则会报错 `handler.construct(target, args, newTarget)`

**deleteProperty** 拦截delete操作, 返回一个布尔值 `handler.deleteProperty(target, propKey)`

**getOwnPropertyDescriptor** 拦截`Object.getOwnPropertyDescriptor`操作,返回属性的描述对象。 `handler.getOwnPropertyDescriptor(target, propKey)`

**defineProperty** 拦截`Object.defineProperty`操作 `handler.defineProperty(target, propKey, propDesc)`

**getPrototypeOf** 拦截获取对象原型， 返回值必须是对象或者null

**setPrototypeOf** 拦截`Object.setPrototypeOf`

**ownKeys** 拦截对象自身属性的读取


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

## Proxy.revocable(target, handler)

返回一个对象`{proxy, revoke}`， proxy是Proxy实例, revoke是可取消Proxy的函数, 取消后再访问Proxy实例会报错
