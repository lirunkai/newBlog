# 数组

基础知识, 列一下api, 然后记录下一些巧妙的用法, 以及一些容易出错的地方.

## 返回新数组

`Array.from(likeArr, fn)`

将类数组转换成数组, 如果提供了fn, 数组内的每一项都会执行fn, 返回一个新数组

`Array.of(element, element1, element2)`

创建一个具有可变数量参数的新数组实例

`x.concat(x1,x2,x3)` ===       [...x, ...x1, ...x2, ...x3]

合并多个数组

`filter(fn)`

返回通过fn的新数组， 没有返回空数组

`map(fn)`

数组中的每一项都运行fn, **返回由fn的返回值组成的新数组, 返回的undefined会保留**

```
let x = [1,2,3,4,5]

x.map(item => {
  if(item > 2){
   return item
  }
})

// [undefined, undefined, 3, 4, 5, 6]
```

`slice(start,end)`

**浅拷贝** 数组的一部分返回， 如果为负数表示倒数第几个

```
// tribonacci([1,2,3],10) => [1,2,3,6,11,20,37,68,125,230]

function tribonacci(signature,n){  
  for (var i = 0; i < n-3; i++) {
    signature.push(signature[i] + signature[i+1] + signature[i+2]);
  }
  return signature.slice(0, n); //return trib - length of n
}
```

`flat(num)`

降num个维度, 如果需要将不知道多少个维度的数组转成一维数组`arr.flat(Infinity)`

`flatMap(fn)`

先循环数组,之后调用flat

## 修改原数组

`splice(start, length, el)`

数组中从start开始删除多个（length)元素， 如果length为0, el有多个是添加

`fill(value, start, end)`

将数组的start到end填充成value, start和end如果是负数（start+length）

`pop()`

从最后删除

`shift()`

从最开始删除

`push()`

插入到最后一位

`unshift()`

插入到首位

`reverse()`

颠倒数组中元素的位置

## 判断

`Array.isArray()`

判断输入是否是数组, 返回true或者false

`every(fn)`

数组的每一项都通过了函数， 返回true

`some(fn)`

数组的某一项通过了函数 返回true

`find(fn)`

返回通过fn的第一个值, 没有一个通过返回undefined

`findIndex(fn)`

返回通过fn的第一个值的索引，没有一个通过返回-1

`indexOf(item)`

查到item在数组中的索引, 没有返回-1

`includes(item, [start])`

查询数组中是否包含item, 返回true或者false, start参数代表从哪里开始查询

## 其他类型

`join()`

将数组中的元素用符号连接起来变成字符串

`reduce(fn， initData)`

使用累加器把数组的值进行累加简化成单个值

fn(累加值，当前值， 当前索引, arr)

`forEach(fn)`

数组中的每个选项都运行fn，**返回undefined,不可链式调用**
