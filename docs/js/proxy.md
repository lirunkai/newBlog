# Proxy（～～收费站）

拦截， 代理。 拦截住了就代理上, 没拦截就通过。

Proxy首先要有对象,或者说需代理对象有defineProperty, get或者set等这些操作之后, Proxy才有意义.

Proxy的用法`new Proxy(target, handler)`

## target(～～车型)

target 要使用Proxy代理的对象， 对象的类型可以是 Object | Function | Array | Proxy

比如

target对象为函数时
```
function sum(a, b) {
  return a + b;
}

const handler = {
  apply(target, thisArg, argumentsList) {
    // 这个就感觉是给你了个小票
    console.log(`${argumentsList}`)
    // target调用
    return target(argumentsList[0], argumentsList[1]) * 10;
  }
}

let proxySum = new Proxy(sum, handler)

let num = proxySum(1, 2);

console.log(num);
```

## handler(～～收费项目)

**get(target, property, receiver)** 

拦截属性的读取

```javascript
let p = new Proxy({a: '1'}, {
	get(target, property, receiver) {
		return target[property]
	}
})

p.a
```



**set(target, property, value)** 

拦截属性的设置, 返回一个布尔值

**apply(target, thisArg, arguments)** 

拦截函数的调用, call和apply操作 

+ `target`  目标函数
+ `thisArg`  被调用时的函数对象
+  `arguments` 被调用时的参数数组

```javascript
const handler = {
	apply(target, thisArg, arguments) {
		return target(arguments[0], arguments[1])
	}
}
```

**has(target, property)** 

拦截HasProperty操作,比如`in, Reflect.has()`， 返回一个布尔值

**construct(target, args)** 

拦截new操作, 返回的必须是一个对象，否则会报错 

`handler.construct(target, args)`

```javascript
const handler = {
  construct(target, args) {
    // add some js
    return new target(...args)
  }
}

class Lnb {}

let lnb = new Proxy(Lnb, handler)
```



**deleteProperty(target, property)** 

拦截delete操作, 返回一个布尔值, 表示是否删除成功

```javascript
let p = new Proxy({a: '1'}, {
	deleteProperty(target, property) {
    return true
  }
})

delete p.a
```



**getOwnPropertyDescriptor**

拦截`Object.getOwnPropertyDescriptor`操作,返回属性的描述对象。 

**defineProperty(target, property, descriptor)** 

拦截`Object.defineProperty`操作, 必须返回一个Boolean, 表示定义该属性的操作成功与否

```javascript
var p = new Proxy({}, {
  defineProperty: function(target, prop, descriptor) {
    console.log('called: ' + prop);
    return true;
  }
});

var desc = { configurable: true, enumerable: true, value: 10 };
Object.defineProperty(p, 'a', desc); // "called: a"
```

**getPrototypeOf** 

拦截获取对象原型， 返回值必须是对象或者null

**setPrototypeOf** 

拦截`Object.setPrototypeOf`

**ownKeys** 

拦截对象自身属性的读取

+ `Object.keys()`
+  `Object.getOwnPropertyNames()`
+  `Reflect.ownKeys()`


## 拦截后

当拦截到我们想拦截的, 我们可以对他们的默认行为进行修改。

```javascript
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

## revocable(~~违建，拆除)

`Proxy.revocable()`

返回一个对象`{proxy, revoke}`， proxy是Proxy实例, revoke是可取消Proxy的函数, 取消后再访问Proxy实例会报错
