# this

整明白this

## 作为函数

作为函数使用时, 指向函数的上下文window对象

## 作为方法

当一个函数被赋值给一个对象的一个属性，并使用引用该函数的这个属性进行调用函数时，那么函数就是作为该对象的一个方法进行调用的， `this` 指向 调用时的对象

## 作为构造器

将函数作为构造器调用时，便会通过这个函数生成一个新对象，这时，this 指向这个新创建的实例

## 使用call apply

在call, apply 中 this指向传入的对象

## ES6

ES6 中，箭头函数中this值， 指向定义时所在的对象

## class

当一个对象调用静态或原型方法时，如果该对象没有“this”值, 那么this值在被调用的函数内部将为`undefined`

因为所有的函数、方法、构造函数、getters或setters都在严格模式下执行. 因此如果我们没有指定this的值, this值将为`undefined`

静态方法中的this, 表示当前类


---

### call的实现

```javascript
Function.prototype.call = function (content){
  // 获取this执行的作用于
  let content = content || window;
  // 获取函数
  content.fn = this;
  //	获取参数
  let args = [...arguments].slice(1)
  // 执行函数
  let result = content.fn(...args)
  delete content.fn
  return result
}
```

### apply的实现

```javascript
Function.prototype.apply = function (content) {
	let content = content || window;
  content.fn = this
  let result;
	if(arguments[1]){
    result = content.fn(arguments[1])
  } else {
    result = content.fn()
  }
  delete content.fn
  return result
}
```

### bind的实现

```javascript
Function.prototype.bind = function (content){
  if (typeof this !== 'function') {
    throw new TypeError('Error')
  }
  let _this = this
  let args = [...arguments].slice(1)
  return function K(){
    if (this instanceof K) {
      return new _this(...args, ...arguments)
    } else {
      return _this.apply(content, args.concat(...arguments))
    }
  }
}
```