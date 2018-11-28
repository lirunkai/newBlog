# 排序算法

这里说一下冒泡排序, 选择排序, 插入排序, 归并排序

## 冒泡排序

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

## 选择排序

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


## 插入排序

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

## 归并排序

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


## 快速排序

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
