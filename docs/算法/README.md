### 算法

### 时间复杂度

大 O 表示法

如何分析时间复杂度？

1. 只关注循环执行次数最多的一段代码

```javascript
function solution(n) {
  let result = [];
  for (let i = 0; i < n; i++) {
    result.push(i);
  }
  return result;
}
```

由于循环执行次数最多的是第 4 行代码， 这行代码被执行了 n 次，所以总的时间复杂度就是 O(n)

```javascript
function solution(n) {
  let result = [];
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      result.push([i, j]);
    }
  }
  return result;
}
```

由于循环执行次数最多的是第 5 行代码， 这行代码被执行了 n\*n 次，所以总的时间复杂度就是 O(n^2)

```javascript
function findX(arr, n) {
  for (let x = 0; x < arr.length; x += 2) {
    if (arr[x] == n) {
      return x;
    }
  }
  return -1;
}
```

由于循环执行次数最多的是第 3,4, 行代码， 这行代码被执行了 n/2 次，所以总的时间复杂度就是 O(logn)

2. 加法法则：总复杂度等于量级最大的那段代码的复杂度

3. 乘法法则: 嵌套代码的复杂度等于嵌套内外代码复杂度的乘积

复杂度量级（递增）

O（1） 常量

O(logn) 对数阶

O(n) 线性

O(n^2) 平方阶级

![](./../_media/大O.jpg)

### 空间复杂度

根据使用的变量大小来定义空间复杂度

### 数据结构

线性表数据结构

**数组**

在内存中连续存储

插入操作 O(n)

删除操作 O(n)

读取 O(1)

#### 写一个数组(包含对象等类型元素)去重数组。

```javascript
// 判断类型
const getType = (function() {
  	const class2type = { '[object Boolean]': 'boolean', '[object Number]': 'number', '[object String]': 'string', '[object Function]': 'function', '[object Array]': 'array', '[object Date]': 'date', '[object RegExp]': 'regexp', '[object Object]': 'object', '[object Error]': 'error', '[object Symbol]': 'symbol' }
		
    return function getType(obj) {
        if (obj == null) {
            return obj + ''
        }
        // javascript高级程序设计中提供了一种方法,可以通用的来判断原始数据类型和引用数据类型
        const str = Object.prototype.toString.call(obj)
        return typeof obj === 'object' || typeof obj === 'function' ? class2type[str] || 'object' : typeof obj
    };
})()

// 判断是否相等
const isEqual = (o1, o2) => {
  const t1 = getType(o1)
  const t2 = getType(o2)
  
  if(t1 != t2) return false
  
  if(t1 === 'array') {
    if(o1.length != o2.length) return false
    return o1.every((item, i) => {
      return isEqual(item, o2[i])
    })
  }
  
  if(t2 === 'object') {
    // object类型比较类似数组
        const keysArr = Object.keys(o1)
        if (keysArr.length !== Object.keys(o2).length) return false
        // 比较每一个元素
        return keysArr.every(k => {
            return isEqual(o1[k], o2[k])
        })
  }
  
  return o1 == o2
}

const removeDuplicates = (arr) => {
  return arr.reduce((accumlator, current) => {
    const hasIndex = accumlator.findIndex(item => isEqual(current, item))
    if(hasIndex === -1) {
      accumlator.push(current)
    }
    return accumlator
  }, [])
}
```



**链表**

[链表](https://leetcode-cn.com/leetbook/detail/linked-list/)（Linked List）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的指针（Pointer）。

**跳表**

链表加**多级索引**的结构，就是跳表

新增， 删除，需要维护其平衡性

**散列表** 也称为哈希表

**栈**

后入先出

使用： 浏览器的前进后退， 函数调用栈

**队列** 

先入先出

使用： 循环队列， 阻塞队列， 并发队列， 排队请求

实现：

基于数组实现的是顺序队列

基于链表实现的是链式队列

循环队列实现时需要注意： 确定好空队列和队满的判定情况

### 贪心算法

在对问题求解时，总是作出对当前最优的解法

贪心算法与动态规划的不同在于它对于每个子问题的解决方案都作出选择，不能回退。

动态规划会保存以前的运算结果，并根据以前的结果对当前进行选择，有回退功能

### 排序算法

#### 冒泡算法

每次都和后一个进行对比, 如果比之后的大, 则互换

``` javascript
function BubbleSort(arr, flag = 0) {
  let len = arr.length
  for(let i = 0; i <len; i++) {
    for(let j = 0; j< len -1 -i; j++) {
      if(arr[j] > arr[j+1]) {
        [arr[j], arr[j+1]] = [arr[j+1], arr[j]]
      }
    }
  }
  return flag ? arr.reverse() : arr
}
```
#### 计数排序

创建统计数组并统计对应元素个数

```javascript
function countingSort(arr) {
	let min = arr[0],
	  	max = arr[0],
      len = arr.length
  for(let i = 0; i < len; i++) {
    max = Math.max(arr[i], max)
    min = Math.min(arr[i], min)
  }
  
  
}
```

#### 快速排序（取中间数）

1. 选择数组中间数作为基数
2. 准备两个数组容器, 遍历数组, 逐个与基数对比, 较小的放左边容器, 较大的放右边容器
3. 递归处理两个容器的元素

```javascript
function quickSort(arr) {
  if(arr.length <= 1) return arr
  let index = Math.floor(arr.length / 2)
  let pivot = arr.splice(index, 1)[0],
      left = [],
      right = []
  for(let i = 0; i < arr.length; i++) {
    if(pivot > arr[i]) {
      	left.push(arr[i])
    } else {
      	right.push(arr[i])
    }
  }
  return quickSort(left).concat([pivot], quickSort(right))
}
```



#### 归并排序

将两个有序数列合并成一个有序数列, 我们称之为**归并**

1. 将数组拆分成A,B两个小组, 两个小组继续拆, 直到每个小组只有一个元素为止
2. 根据拆分过程逐步合并小组, 由于各小组初始只有一个元素, 可以看作小组内部是有序的, 合并小组可以被看作是合并两个有序数组的过程
3. 对左右两个小数列重复第二步, 直至各区间只有一个数

```javascript
function merge(left, right) {
  let result = []
  while(left.length && right.length) {
    if(left[0] <= right[0]) {
      result.push(left.shift())
    } else {
      result.push(right.shift())
    }
  }
  while(left.length) {
    result.push(left.shift())
  }
  while(right.length) {
    result.push(right.shift())
  }
  return result
}

function mergeSort(arr) {
  if(arr.length <= 1) {
    return arr
  }
  let mid = Math.floor(arr.length / 2)
  let left = arr.slice(0, mid),
      right = arr.slice(mid)
  let mergeLeftArray = mergeSort(left),
      mergeRightArray = mergeSort(right)
  return merge(mergeLeftArray, mergeRightArray)
}
```

#### 插入排序

通过构建有序序列, 对于未排序数据, 在已排序序列中从后向前扫描, 找到相应位置并插入

1. 从第一个元素开始, 该元素可以认为已经被排序
2. 去除下一个元素, 在已排序的元素序列中从后向前扫描
3. 如果已排序元素大于新元素, 将该元素移到下一个位置
4. 重复

```javascript
function insertionSort(arr) {
  let len = arr.length
  
  for(let i = 0; i< len; i++) {
	    let preIndex = i - 1,
          cur = arr[i]
      while(preIndex >= 0 && arr[preIndex] > cur) {
        arr[preIndex + 1] = arr[preIndex]
        preIndex --;
      }
	    arr[preIndex + 1] = cur
  }
  
  return arr
}
```

#### 选择排序

每次选择最小的添加到排序数组

```javascript
function selectSort(arr) {
  let len = arr.length,
      temp = 0
  
  for(let i = 0; i < len; i++) {
    temp = i
    for(let j = i+ 1; j< len; j++) {
      if(arr[j] < arr[temp]) {
        temp = j
      }
    }
    
    if(temp !== i) {
      [arr[i], arr[temp]] = [arr[temp], arr[i]]
    }
  }
  
  return arr
}
```

