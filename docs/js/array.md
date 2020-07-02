## Iterator 迭代器

Iterator（迭代器）是一种接口，也可以说是一种规范。为各种不同的数据结构提供统一的访问机制。

任何数据结构只要部署Iterator接口（js中的[Symbol.iterator]），就可以完成遍历操作

1. 为各种数据结构，提供一个统一的、简便的访问接口；
2. 使得数据结构的成员能够按某种次序排列
3. ES6 创造了一种新的遍历命令for…of循环，Iterator 接口主要供for…of消费。

## 数组

基础知识, 列一下api, 然后记录下一些巧妙的用法, 以及一些容易出错的地方.

### 返回新数组

`Array.from(likeArr, fn, this)`

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

### 修改原数组

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

 为数组中的每一个元素执行一次 `fn` 函数，直到找到一个使得 callback 返回一个“真值”（即可转换为布尔值 true 的值）。如果找到了这样一个值，`some()` 将会**立即返回** `true`。否则，`some()` 返回 `false`。也就是说some找到为true的元素后不会再向下执行

`find(fn)`

返回通过fn的第一个值, 没有一个通过返回undefined

`findIndex(fn)`

返回通过fn的第一个值的索引，没有一个通过返回-1

`indexOf(item)`

查到item在数组中的索引, 没有返回-1

`includes(item, [start])`

查询数组中是否包含item, 返回true或者false, start参数代表从哪里开始查询

### 其他类型

`join()`

将数组中的元素用符号连接起来变成字符串

`reduce(fn， initData)`

使用累加器把数组的值进行累加简化成单个值

fn(累加值，当前值， 当前索引, arr)

`forEach(fn)`

数组中的每个选项都运行fn，**返回undefined,不可链式调用**

---

## Set

Set定义一个新的数据结构, 内部的值没有重复的, 也就是没有全等的值.

```
// 一行代码为数组去重

[...new Set(arr)]
```

### 属性

`size`  类似数组的length, 表明Set里有多少个数据

### 方法

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

### 遍历

`keys()` 返回键名

`values()` 返回键值

`entries()` 返回键值对

由于Set是类数组， 所以可以使用`Array.from()`来转成数组去使用数组的方法



---

## 扩展数据结构:

### 队列(FIFO first-in-first-out)

先入先出的数据结构 first-in-first-out

```javascript
// js实现
class Queue {
  constructor() {
    this.equeue = []
  }
  
  isEmpty() {
    return this.equeue.length == 0
  }
  
  size() {
    return this.equeue.length
  }
  
  dequeue() {
    return this.equeue.shift()
  }
  
  enqueue(item) {
    this.equeue.push(item)
  }
  
}
```

循环队列

length固定,  主要控制 首部指针和尾部指针来进行插入

```javascript
class ReQueue {
  constructor(k) {
    this.size = k
    this.head = -1
    this.tail = -1
    this.data = []
  }
	isFull() {
    return (this.tail + 1)%this.size === this.head
  }
  isEmpty() {
    return this.tail === -1 && this.head === -1
  }
  Front() {
    return this.head === -1 ? -1 : this.data[this.head]
  }
  Rear() {
    return this.tail === -1 ? -1 : this.data[this.tail]
  }
  enQueue(value) {
    if(this.isFull()) {
      return false
    }
    if(this.isEmpty()) {
      this.head = 0
    }
    this.tail = (this.tail + 1)%this.size
    this.data[this.tail] = value
    return true
  }
  deQueue() {
    if(!this.isEmpty()) {
      if(this.tail === this.head) {
        this.tail = -1
        this.head = -1
      } else {
        this.head = (this.head + 1)%this.size
      }
      return true
    }
    return false
  }
}
```

矩形变换

```javascript
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function(matrix) {
    let m = matrix.length, n = matrix[0].length
    for(let i = 0; i < m; i++) {
        for(let j = 0; j < i; j++) {
            let temp = matrix[i][j]
            matrix[i][j] = matrix[j][i]
            matrix[j][i] = temp
        }
    }
    for(let i = 0; i < m; i++) {
        for(let j = 0; j < n/2; j++) {
            let temp = matrix[i][j]
            matrix[i][j] = matrix[i][n-j-1]
            matrix[i][n-j-1] = temp 
        }
    }
    return matrix
};
```

零矩阵

```javascript
/**输入：
[
	[1,1,1],
	[1,0,1],
	[1,1,1]
]
输出：
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
*/
var setZeroes = function(matrix) {
    let rowZero = new Set()
    let colZero = new Set()
    matrix.forEach((item, index) => {
        if(item.includes(0)) {
            rowZero.add(index)
        }
        item.forEach((oo, index2) => {
            if(oo == 0) {
                colZero.add(index2)
            }
        })
    })
    Array.from(rowZero).forEach(row => {
        matrix.forEach((item, index) => {
            if(rowZero.has(index)) {
                matrix[index].fill(0)
            }
            item.forEach((col, chindex) => {
                if(colZero.has(chindex)) {
                    matrix[index][chindex] = 0
                }
            })
        })          
    })
    return matrix
};
```

对角线遍历

```javascript
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var findDiagonalOrder = function(matrix) {
    // 设m为纵坐标，n为横坐标
    // 据题意可知，当m+n为奇数时向下遍历，m+n为偶数时向上遍历
    
    // 遍历方式
    // 向上遍历时：m递减，n递增
    // 向下遍历时：m递增，n递减
    // 以此循环
    
    /** 遍历结束条件
     *  向上遍历：m递减到0或者n递增到最大值
     *  向下遍历：n递减到0或者m递增到最大值
     */
    
    // 初始化返回值
    let res = [];
    let m = matrix.length;
    // 判断输入值长度为0直接返回
    if (m === 0 || (m > 0 && matrix[0].length === 0)) return res;
    let n = matrix[0].length;
    // 定义Boolean traversal值为此时的遍历方式为向上还是向下
    let traversal = true;
    // 循环
	for (let i = 0; i < m + n - 1; i++)
	{
		let pm = traversal ? m : n;
		let pn = traversal ? n : m;

        // 保证了x + y = i;
		let x = (i < pm) ? i : pm - 1;
		let y = i - x;                

		while (x >= 0 && y < pn)
		{
			res.push(traversal ? matrix[x][y] : matrix[y][x]);
			x--;
			y++;
		}

		traversal = !traversal;
	}
	return res;
};
```

### 栈(FILO first-in-last-out)

---

### 排序算法

#### 冒泡排序

将数组的每一项与后一项进行对比, 如果不符合要求就交换位置, 一共遍历n(数组的长度)轮, 会进行n*n次对比.

js实现

```
function popo(arr){
  let len = arr.length;
  for(let i = 0; i< len; i++){
    for(let j = 0; j< len; j++){
      if(arr[j] > arr[j+1]){
        [arr[j], arr[j+1]] = [arr[j+1], arr[j]]
      }
      console.count('bad')
    }
  }
  return arr;
}

popo([1,3,2,5,4,10])
// count执行了36次 最后输出 [1,2,3,4,5,10]
```

优化: 每次遍历之后, 结尾的符合规则的其实已经不会变了, 不需要再进行对比。

```
function popo(arr){
  let len = arr.length;
  for(let i = 0; i< len; i++){
    for(let j = 0; j< len - 1 - i; j++){
      if(arr[j] > arr[j+1]){
        [ arr[j], arr[j+1] ] = [ arr[j+1], arr[j] ]
      }
      console.count('perfet')
    }
  }
  return arr;
}

popo([4,3,1,2,10])
// count执行了10次, 不优化的会执行25次
// 输出[1,2,3,4,10]

```

#### 选择排序

选择排序就比较好理解了, 在数组中找到最大值或者最小值, 放到第一位, 再从剩余的数组中找最大值, 放到第二位, 。。。哔哔哔。

js实现

```
function choose(arr){
  let len = arr.length;
  for(let i =0; i< len; i++){
    let max = i;
    for(let j =i; j< len; j++){
      if(arr[j] > arr[i]){
        max = j;
      }
    }
    if(max !== i){
      [arr[max], arr[i]] = [arr[i], arr[max]]
    }
  }
  return arr;
}
```

```
function choose(arr){
  let newArr = [];
  function loop(arr){
    if(arr.length){
      let max = Math.max(...arr)
      for(let i = 0; i< arr.length; i++){
        if(arr[i] == max){
          newArr.push(arr[i])
          arr.splice(i, 1)
          console.log(arr)
          break;
        }
      }
      loop(arr)
    }  
  }
  loop(arr)
  return newArr;
}
```

#### 插入排序

从数组的第二项开始遍历数组的`n-1`项. 遍历过程中对当前项的左边数组项, 依次从右向左对比, 如果左边选项大于当前项, 则左边项向右移动, 继续进行比较, 直到找到不大于自身的选项为止。

```
function insertSort(arr){
  let len = arr.length;
  for(let i =0; i< len; i++){
    let j = i;
    let tmp = arr[j] // 获取对比的值
    while(j > 0 && arr[j -1] > tmp){ // 左边比右边大
      arr[j] = arr[j - 1] // 右边的赋值为左边的
      j--
    }
    arr[j] = tmp //在最后对比的地方 给j索引赋值
  }
}
```

#### 归并排序

将复杂的数组进行多次分解， 分解为多个小型数组进行合并. 关键是怎么去合并

```
function mergeSort(arr){
  function splitFn(arr){
    if(arr.length == 1) return arr;
    let mid = Math.floor(arr.length/2)
    let left = arr.slice(0, mid)
    let right = arr.slice(mid)
    return merge(splitFn(left), splitFn(right))
  }

  function merge(left, right){
    let ileft = 0, jright = 0, result = [];
    while(ileft < left.length && jright < right.length){
      if(left[ileft] < right[jright]){
        result.push(left[ileft++])
      } else {
        result.push(right[jright++])
      }
    }
    return result.concat(left.slice(ileft)).concat(right.slice(jright))
  }
  return splitFn(arr)
}

```

#### 快速排序

1. 在数组中选择一个参考点, 然后对于数组的每一项, 大于point点的放右边， 小于的放左边.
2. 重复对左右进行第一步操作, 直到左右的数组长度为1

```
function soonSort(arr){
  if(arr.length <= 1) return arr;
  return [
    ...soonSort(arr.slice(1).filter(item => item < arr[0])),
    arr[0],
    ...soonSort(arr.slice(1).filter(itme => item > arr[0]))
  ]
}
```

还有随机快速排序, 计数排序