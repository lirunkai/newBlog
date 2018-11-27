# Set

Set定义一个新的数据结构, 内部的值没有重复的, 也就是没有全等的值.

```
// 一行代码为数组去重

[...new Set(arr)]
```

## 属性

`size`  类似数组的length, 表明Set里有多少个数据

## 方法

`set.add()` 添加一个值到set里, 返回set结构本身

```
由于返回了Set结构本身 所以可以进行链式添加

let s = new Set()

s.add(1).add(2).add(2)
// s.size 为 2
```

`set.delete()` 返回Boolean值， 表示是否删除成功

`set.has()` 返回Boolean值, 表示Set中是否有这个数据

`set.clear()` 清空set 无返回值

## 遍历

`keys()` 返回键名

`values()` 返回键值

`entries()` 返回键值对

由于Set是类数组， 所以可以使用`Array.from()`来转成数组去使用数组的方法
