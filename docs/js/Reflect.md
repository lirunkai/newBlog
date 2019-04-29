# Reflect

个人对Reflect的理解就是把Object的一些方法归类, 归属到Reflect类下面, 让Reflect更加的纯粹, 实现更加合理

## Reflect.has(obj, name)

等同于`name in obj`

## Reflect.deleteProperty(obj, name)

等同于 `delete obj[name]`，返回一个布尔值, 表示是否删除成功

## Reflect.get(target, name, receiver)

查找target[name], 如果有值进行返回, 如果没有值返回undefined。

如果name绑定了读取函数(getter)， 则this绑定receiver

## Reflect.set(target, name, value, receiver)

设置target[name]的值为value.

如果name设置了赋值函数, 则this绑定receiver

## Reflect.construct(target, args)

等同于`new target(...args)`， 提供了一种不使用`new`来调用构造函数的方法

## Reflect.getPrototypeOf(obj)

读取对象的__proto__属性

## Reflect.setPrototypeOf(obj, newProto)

设置对象的__proto__属性， 如果无法设置返回false

## Reflect.defineProperty(target, propertyKey, attributes)

为对象定义属性

## Reflect.getOwnPropertyDescriptor(target, propertyKey)

获取对象指定属性的描述对象

## Reflect.apply(func, thisArgs, args)

绑定this对象后执行给定函数，等同于`fn.apply()`

## Reflect.isExtensible(target)

表示当前对象是否可扩展

## Reflect.preventExtensions(target)

让一个对象变为不可扩展, 返回一个布尔值, 表示是否操作成功

## Reflect.ownKeys(target)

返回对象的所有属性，包括`Symbol`
