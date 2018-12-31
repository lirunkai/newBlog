# Promise

Promise， 异步流程控制之一, 解决回调地狱.

## 状态

`pending` 进行中

`fulfilled` 成功

`rejected` 失败

### Promise构造函数

创建一个实例 `let promise = new Promise((resolve, reject) => resolve())`

`resolve`函数

如果`resolve`是一个`Promise`，当前`Promise`的状态将根据`resolve（promise）`的状态来切换

如果`resolve`一个非`Promise`实例，将`Promise`的状态从`pending`切换到`fulfilled`

`reject`函数 将Promise的状态从`pending`切换到`rejected`

`Promise`新建后会立即执行, 是一个同步的执行过程

### then

`Promise`实例状态改变时的回调函数 `then`返回一个新的`Promise`实例

### catch

处理之前then里面的报错, catch也会返回一个Promise实例。

### all

将多个`promise`实例, 包装成一个`promise`实例

比如我们有p1, p2, p3多个promise实例, 生成`pAll` 一个`promise`实例

只有p1, p2, p3的状态都变成fulfilled之后, `pAll`的状态才会变成`fulfilled`

如果p1, p2, p3的其中一个状态变成rejected, `pAll`的状态变成`rejected`

类似 `&&` 的策略

### race

race和all相反

如果有一个状态变成`fulfilled`， race生成的`pAll`的状态为`fulfilled`, 且参数是优先改变的promise的返回值

如果p1, p2, p3的状态都变成`rejected`, `pAll`的状态才为`rejected`

### finally

不管对象的状态如何, 最终都会执行， 不接受任何参数

### Promise.resolve()

如果传参是一个`Promise`，当前`Promise`的状态将根据`resolve（promise）`的状态来切换

如果传参一个非`Promise`实例，将`Promise`的状态从`pending`切换到`fulfilled`

### Promise.reject()

返回新的`Promise`实例，该实例的状态为`rejected`

### 注意

`resolve()` 后的代码还会执行, 但是 `return resolve()`之后的代码不会执行


## 实现

```
const isFunction = isFn => typeof isFn === 'function'

class MyPromise {
  constructor(handler){

    // 传参必须是函数
    if(!isFunction(handler)) {
      throw new Error('Promise must accept a function as paramer')
    }

    // 状态 Pending Fulfilled Rejected
    this._status = "Pending"
    this._value = undefined
    this._fulfilledQueues = []
    this._rejectedQueues = []

    try{
      handler(this._resolve.bind(this), this._reject.bind(this))
    } catch(err) {
      this._reject(err)
    }

  }
  _resolve(val){

    const run = () => {
      if(this._status !== 'Pending') return
      const runFulfilled = (value) => {
        let cb;
        while(cb = this._fulfilledQueues.shift()){
          cb(value)
        }
      }

      const runRejected = (error) => {
        let cb;
        while(cb = this._rejectedQueues.shift()){
          cb(error)
        }
      }

      if(val instanceof MyPromise){
        val.then(value => {
          this._value = value
          this._status = "Fulfilled"
          runFulfilled(value)
          }, err => {
            this._value = err
            this._status = 'Rejected'
            runRejected(err)
            })
      } else {
        this._value = val
        this._status = 'Fulfilled'
        runFulfilled(val)
      }
    }

    setTimeout(run, 0)
  }

  _reject(err){
    if(this._status != 'Pending') return
    const run = () => {
      this._status = 'Fulfilled'
      this._value = val
      let cb
      while(cb = this._rejectedQueues.shift()){
        cb(val)
      }
    }

    setTimeout(() => run(), 0)
  }

  then (onFulfilled, onRejected) {
    const { _value, _status } = this
    return new MyPromise(onFulfilledNext, onRejectedNext) => {
      // Fulfilled
      let fulfilled = value => {
        try {
          if(!isFunction(onFulfilled)){
            onFulfilledNext(value)
          } else {
            let res = onFulfilled(value)
            if(res instanceof MyPromise){
              //
              res.then(onFulfilledNext, onRejectedNext)
            } else {
              onFulfilledNext(res)
            }
          }
        } catch(err){
          onRejectedNext(err)
        }
      }

      let rejected = error => {
        try {
          if(!isFunction(onRejected)){
            onRejectedNext(error)
          } else {
            let res = onRejected(error)
            if(res instanceof MyPromise){
              res.then(onFulfilledNext, onRejectedNext)
            } else {
              onFulfilledNext(res)
            }
          }
        } catch (err){
          onRejectedNext(err)
        }
      }

      switch(_status){
        case 'Pending':
          this._fulfilledQueues.push(fulfilled)
          this._rejectedQueues.push(rejected)
          break;
        case 'Fulfilled':
          fulfilled(_value)  
          break;
        case 'Rejected':
          rejected(_value)
          break;
      }
    }
  }

  catch(onRejected){
    return this.then(undefined, onRejected)
  }

  static resolve(value){
    if(value instanceof MyPromise) return value
    return new MyPromise(resolve => resolve(value))
  }

  static reject(value){
    return new MyPromise((resolve, reject) => reject(value))
  }

  static all(list){
    return new MyPromise((resolve, reject) => {
      let values = []
      let count = 0;
      for(let [i, p] of list.entries()){
        this.resolve(p).then(res => {
            values[i] = res
            count++
            if(count === list.length) resolve(values)
        }, err => {
          reject(err)
        })
      }
    })
  }

  static race(list){
    return new MyPromise((resolve, reject) => {
      for(let p of list){
        this.resolve(p).then(res => {
            resolve(res)
        }, err => {
          reject(err)
        })
      }
    })
  }  

  static finally(cb){
    return this.then(
        value => MyPromise.resolve(cb()).then(() => value),
        reason => MyPromise.rresolve(cb()).then(() => {throw reason})
    )
  }  
}
```
