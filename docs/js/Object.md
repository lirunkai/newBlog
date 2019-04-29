## 面向对象编程(OOP)

一种在程序中包含各种独立而又互相调用的对象的思想

对象指的是类的实例。它将对象作为程序的基本单元，将程序和数据封装其中，以提高软件的重用性、灵活性和扩展性，对象里的程序可以访问及经常修改对象相关连的数据.

## Object

`Object.assign(target, sources)`

用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

属于浅拷贝

无法复制深层属性, 比如

```javascript
Object.assign({url: {'a': "v"}}, {url: {'b': 'd'}})
// {url: {b: "d"}}
// 可以使用lodash
_.defaultsDeep(object, source)
_.defaultsDeep({ 'user': { 'name': 'barney' } }, { 'user': { 'name': 'fred', 'age': 36 } });
// { 'user': { 'name': 'barney', 'age': 36 } }
```


`Object.create(prototype, propertiesObject)` 创建一个对象

`Object.freeze(obj)`    冻结一个对象， 不能添加， 修改， 删除属性.

`Object.seal(obj)`    防止其他代码删除对象的属性

`Object.isExtensible()` 是否可扩展

`Object.isFrozen()` 是否冻结

`Object.isSealed()` 是否密封

`Object.getOwnPropertyNames(obj)`  指定对象的所有自身属性的属性名， 包含不可枚举的属性但不包括Symbol值作为属性名的

`Object.getOwnPropertySymbols(obj)` 对象自身的所有`Symbol`属性的数组

`Object.keys()` 返回所有可枚举的属性名

`Object.values()` 返回对象自身可枚举值的数组

`Object.getPrototypeOf(obj)`获取对象的原型

`Object.setPrototypeOf(obj, prototype)` 设置对象的原型

-------------

`Object.defineProperty(obj, prop, descriptor)`

在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

`descriptor`

  1. `configurable` 当且仅当该属性的`configurable`为`true`时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为`false`

  2. `enumerable`  为`true`时可枚举, 默认为false

  3. `get`  获取对象的属性值时触发, 方法执行时没有参数传入

  4. `set`  设置对象的属性值时触发, 该方法将接受唯一参数，即该属性新的参数值

  5. `writable` 当且仅当为true时, `value`才能被赋值运算符修改, 默认为false

  6. `value` 属性对应的值 默认是 undefined

----------------

`Object.is(n1, n2)` 判断两个值是否相同

​	和`===`不同的是，可以判断`-0 +0`, `NaN`

----------------
