# Symbol

1. Symbol 类型, ES6新增的一种原始类型.

2. Symbol 独一无二， 代表某个变量是独一无二的。

所以

```
let s1 = Symbol('a')
let s2 = Symbol('a')

s1 === s2 // false
```

3. 不能用点来操作

4. Symbol值的引用需要保存变量. 比如

```
let s = Symbol('a')
let obj = {
  [s]: 'a'
}

console.log(obj[s])
```

## 遍历

1. 可以通过`Object.getOwnPropertySymbols()`来获取对象的所有属性名是`Symbol`值。

2. 可以通过`Reflect.ownKeys()`方法来获取所有属性名， 包含常规属性和Symbol属性

无法通过`for in` `Object.keys()`来获取

## 需要重复使用的话

需要使用`Symbol.for(key)`去注册一个key

`Symbol.for(key)`如果注册过, 返回注册后的值, 如果没注册, 进行注册

```
let key1 = Symbol.for('key')
let key2 = Symbol.for('key')

key1 === key2 // true
```

## 获取注册时的key

`Symbol.keyFor()`

```
let key1 = Symbol.for('key')
Symbol.keyFor(key1) //key
```
