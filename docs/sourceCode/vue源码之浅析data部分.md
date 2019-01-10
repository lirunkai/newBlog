# data

用来声明响应式数据

在vue2.0中通过使用`Object.defineProperty()`来做的

比如我们想将一个对象变成可响应式的对象, 也就是我们想观察对象的属性值的变动.

怎么做呢? 通过·Object.defineProperty()·

```
function War(dataObj){
  let signals = {}

  observerData(dataObj)  

  return {
    data:dataObj,
    observe,
    notify
  }
  // 注册监听的通知函数
  function observe(property, signalHandler){
    if(!signals[property]) signals[property] = []
    signals[property].push(signalHandler)
  }
  // 通知
  function notify(signal){
    if(!signals[signal] || signals[signal].length < 1) return
    signals[signal].forEach((signalHandler) => signalHandler())
  }
  // 将普通对象转换成可监听对象
  function makeReactive(obj, key){
    let val = obj[key]

    Object.defineProperty(obj, key, {
      get (){
        return val;
      },

      set (newval){
        val = newval
        notify(key)
      }
    })
  }

  function observerData(obj){
    for(let key in obj){
      if(obj.hasOwnProperty(key)){
        makeReactive(obj, key)
      }
    }
  }
}


let obj = new War({firstName: '2'})

obj.observe('firstName', () => console.log('firstname add handler'))

obj.data.firstName = '3'

// console firstname add handler
```
