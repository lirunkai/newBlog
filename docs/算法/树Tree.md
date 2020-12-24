
### 树

最顶极节点称为 根节点

完全二叉树： 每个节点都有两个子节点

```python
class TreeNode:
  def __init__(self, val):
    self.val = val
    self.left, self.right = None, None
```

### 树的三种遍历

#### 前序遍历 Pre-order 根 - 左 - 右

js实现

```javascript
let res = []
function preOrder(node) {
  res.push(node.val)
  if(node.left) preOrder(node.left)
  if(node.right) preOder(node.right)
}

preOrder(root)
```

python实现

```python
def preorder(self, root):
  if root:
    self.traverse_path.append(root.val)
    self.preorder(root.left)
    self.preorder(root.right)
```

#### 中序遍历 In-order 左 - 根 - 右

js实现

```javascript
function inOrder(node) {
  if(node.left) inOrder(node.left)
  res.push(node.val)
  if(node.right) inOrder(node.right)
}
```

python实现

```python
def inorder(self, root):
  if root:
    self.inorder(root.left)
    self.traverse_path.append(root.val)
    self.inorder(root.right)
```

#### 后序遍历 Post-order 左 - 右 - 根

```javascript
function postOrder(node) {
  if(node.left) postOrder(node.left)
  if(node.right) postOrder(node.right)
  res.push(node.val)
}
```

python实现

```python
def postorder(self, root):
  if root:
    self.postorder(root.left)
    self.postorder(root.right)
    self.traverse_path.append(root.val)
```

#### 层序遍历,一层接一层，从左到右

思路： 借助queue队列, 左子节点先入队, 右子节点后入

```javascript
function levelOrder(root) {
  let res = []
  let queue = [root]
  while(queue.length) {
    let curr = []
    let temp = []
    while(queue.length) {
      let node = queue.shift()
      if(node) {
        curr.push(node.val)
        if(node.left) temp.push(node.left)
        if(node.right) temp.push(node.right)
      }
    }
    curr.length && res.push(curr)
    queue = temp
  }
  return res
}
```

#### 二叉树的右侧视图

```javascript
function rightSideView(root) {
  let arr = []
	function traverse(node, dep) {
    if(node) {
      if(!arr[dep]) {
        arr[dep] = []
      }
      arr[dep].push(node.val)
      traverse(node.left, dep + 1)
      traverse(node.right, dep + 1)
    }
  }
  traverse(root, 0)
  let res = []
  arr.forEach(item => {
    res.push(item[item.length - 1])
  })
  return res
}
```

#### 二叉树最近公共祖先

递归解法

```python
def lowestCommonAncestor(self, root, p, q):
  if p.val < root.val > q.val:
    return self.lowestCommonAncestor(root.left, p, q)
  if p.val > root.val < q.val:
    return self.lowestCommonAncestor(root.right, p, q)
  return root
```

while 循环 和递归一样

```python
def lowestCommonAncestor(self, root, p, q):
  while root:
    if p.val < root.val > q.val:
      root = root.left
    if p.val > root.val < q.val:
      root = root.right
    else:
      return root
```

#### N叉树的前序遍历

```python
class Solution:
    def preorder(self, root: 'Node') -> List[int]:
      if root is None:
        return []
      
      stack, res = [root,], []
      while stack:
        root = stack.pop()
        res.append(root.val)
        stack.extend(root.children[::-1])
      return res
```

### 二叉搜索树 

二叉搜索树:

1. 左子树上所有结点的值均小于它的根结点的值

2. 右子树上所有结点的值均大于它的根结点的值

特殊情况下的二叉搜索树：

子节点都在左子树， 子节点都在右子树， 查找的时间复杂度退化为 O（n）

为了解决这个问题 出现了红黑树

#### 验证二叉搜索树

一个二叉搜索树具有如下特征：
  节点的左子树只包含小于当前节点的数。
  节点的右子树只包含大于当前节点的数。
  所有左子树和右子树自身必须也是二叉搜索树。

```javascript
function isValidBST(root) {
  let order = []
  function inOrder(node) {
    if(node) {
      inOrder(node.left)
      order.push(node.val)
      inOrder(node.right)
    }
  }
  inOrder(root)
  for(let i = 0; i< order.length -1; i++) {
    if(order[i] >= order[i+1]) {
      return false
    }
  }
  return true
}
```

解法1: 中序遍历
```python
class Solution:
  def isValidBST(self, root: TreeNode) -> bool:
    res = []
    def inorder(root):
      if root is None: return
      inorder(root.left)
      res.append(root.val)
      inorder(root.right)
    inorder(root)
    return res == sorted(res) and len(set(res)) == len(res)
```
解法2: 动态更新上界和下界

当前节点的值是其左子树的值的上界（最大值）
当前节点的值是其右子树的值的下界（最小值）

```python
class Solution:
  def isValidBST(self, root: TreeNode) -> bool:
    return self.dg(root, -(2**32), 2**32)
  
  def dg(self, root, min_v, max_v):
    if root is None:
      return True
    
    if root.val < max_v and root.val > min_v:
      pass
    else:
      return False

    if self.dg(root.left, min_v, root.val) == False:
      return False

    if self.dg(root.right, root.val, max_v) == False:
      return False

    return True
```

#### 二叉搜索树中搜索节点

```javascript
function searchNode(root, val) {
  function traverse(node) {
    if(node) {
      if(node.val == val) {
        return node
      } else if(node.val < val) {
        return traverse(node.right)
      } else {
        return traverse(node.left)
      }
    } else {
      return node
    }
  }
  return traverse(root)
}
```

### 堆

#### 什么是堆?

+ 堆是一个完全二叉树
+ 堆上的任意节点值都必须大于等于(大顶堆)或小于等于(小顶堆)其左右节点值

#### 创建大顶堆

通过数组来存储大顶堆，给定一个节点的下标i（i从1开始）,那么它的父节点一定是i/2, 左子节点是2i, 右子节点是2i+1

##### 插入式创建

+ 将节点插入到队尾
+ 与父节点比较, 如果大于父节点(大顶堆)或者小于父节点(小顶堆)，则交换位置
+ 重复上一步, 直到交换到根节点。 插入完成

> Talk is cheap, show me the code

```javascript
function insert(key) {
	  items.push(key)
  	let i = items.length - 1
    while(i/2 > 0 && items[i] > items[i/2]) {
      swap(items, i, i/2)
      i = i/2
    }
}

function swap(arr, i, j ) {
  let temp = items[i]
  items[i] = items[j]
  items[j] = temp
}
```



##### 原地建堆

自下而上式堆化： 将节点和父节点比较, 如果节点大于父节点(大顶堆)或小于父节点(小顶堆),则节点与父节点调整位置

自上而下式: 将节点与其左右子节点比较, 如果存在左右子节点大于该节点(大顶堆)或节点小于该节点（小顶堆）,则将子节点的最大值(大顶堆)或最小值(小顶堆)与之交换

自下而上

```javascript
function buildHeap(items, heapSize) {
  while(heapSize < items.length - 1) {
    heapSize++
    heapify(items, heapSize)
  }
}

function heapify(items, i) {
  while(Math.floor(i/2) > 0 && items[i] < items[Math.floor(i/2)]) {
    swap(items, i, Math.floor(i/2))
    i = Math.floor(i/2)
  }
}

function swap(items, i, j) {
  let temp = items[i]
  items[i] = items[j]
  items[j] = temp
}
```

自上而下

```javascript
function buildHeap(items, heapSize) {
  for(let i = Math.floor(heapSize/2); i >= 1; --i) {
    heapify(items, heapSize, i)
  }
}

function heapify(items, heapSize, i) {
  while(true) {
    var minIndex = i
    if(2*i <= heapSize && items[i] > items[2*i]) {
      minIndex = i*2
    }
    if(2*i +1 <= heapSize && items[minIndex] > items[i*2 +1]) {
      minIndex = i*2 + 1
    }
    if(minIndex === i) break;
    swap(items, i, minIndex)
    i = minIndex
  }
}

function swap(items, i, j) {
  let temp = items[i]
  items[i] = items[j]
  items[j] = temp
}
```



---



1. 最小的K个数

输入整数数组`arr`，找出其中最小的`k`个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

解法一： 数组排序

```javascript
let newsort = arr.sort()
return newsort.slice(0, k)
```

解法2: 构建大顶堆

+ 大顶堆上的任意节点值都必须大于等于其左右子节点值
+ 取出k个数构建大顶堆
+ 从k位开始遍历数组, 如果比堆顶元素进行比较, 大于不做处理, 小于则替换, 然后构建新的大顶堆
+ 遍历完成后, 堆中的数据就是前k小的数据

```javascript
function getLeastNumbers(arr, k) {
	let heap = [,], i = 0
  while(i < k) {
    heap.push(arr[i++])
  }
  buildHeap(heap, k)
  
  for(let i = k; i< arr.length; i++) {
    if(heap[1] > arr[i]) {
      heap[1] = arr[i]
      heapify(heap, k, 1)
    }
  }
  
  heap.shift()
  return heap
}

// 从上而下式建堆 原地建堆
function buildHeap(arr, k) {
  if(k == 1) return
  // i 是父节点 k是子节点
  for(let i = Math.floor(k/2); i>=1; i--) {
    heapify(arr, k, i)
  }
}

// 堆化
function heapify(arr, k, i) {
  while(true) {
    let maxIndex = i
    if(2*i <= k && arr[2*i] > arr[i]) {
      maxIndex = 2*i
    }
    if(2*i+1 <= k && arr[2*i+1] > arr[maxIndex]) {
      maxIndex = 2*i +1
    }
    if(maxIndex !== i) {
      swap(arr, maxIndex, i)
      i = maxIndex
    } else {
      break;
    }
  }
}

function swap(arr, i, j) {
  let temp = arr[i]
  arr[i] = arr[j]
  arr[j] = temp
}


```

2. 前K个高频元素

给定一个非空的整数数组，返回其中出现频率前 **k** 高的元素。

解法一：map+ 数组

```javascript
let topKFrequent = function(nums, k) {
  let map = new Map(), arr = [...new Set(nums)]
  nums.map(num => {
    if(map.has(num)) map.set(num, map.get(num) + 1)
    else map.set(num, 1)
  })
  
  return arr.sort((a, b) => map.get(b) - map.get(a)).slice(0, k)
}
```

解法二：map + 小顶堆

重要的是堆的概念， 之后考虑我们要前K个高频数字, 说明堆里面存的都是数量最大的。

为什么不用大顶堆？ 大顶堆的根节点是最大的。如果在初始化的时候存在最大的，那之后的循环便没有意义。

+ 遍历数据, 统计每个元素出现的频率，并将元素(key)与出现的频率（value）保存到map中
+ 遍历map, 将前k个数, 构造一个小顶堆
+ 从k位开始, 继续遍历map， 每一个数据出现频率都和小顶堆的堆顶元素出现频率进行比较。
+ 小于不做处理，大于替换，重新构建堆
+ 遍历完成后, 堆中的数据就是前K大的数据

```javascript
let topKFrequent = function(nums, k) {
  let map = new Map(), heap = [,]
  nums.map(num => {
    if(map.has(num)) map.set(num, map.get(num) + 1)
    else map.set(num, 1)
  })
  
  if(map.size <= k) {
    return [...map.keys()]
  }
  
  let i = 0
  map.forEach((value, key) => {
    if(i < k) {
      heap.push(key)
      if(i == k -1) buildHeap(heap,map,k)
    } else if(map.get(heap[1]) < value) {
      heap[1] = key
      heapify(heap, map, k ,1)
    }
    i++
  })
  
  heap.shift()
  return heap
}

// 从上而下式堆化 
function buildHeap(heap, map, k) {
  if(k == 1) return
  for(let i = Math.floor(k/2); i>=1; i--) {
    heapify(heap, map, k, i)
  }
}

function heapify(heap, map, k, i) {
  while(true) {
    let minIndex = i
    const leftI = 2 *i
    const rightI = 2* i + 1
    if(leftI < k && map.get(heap[leftI]) < map.get(heap[i])) {
      minIndex = leftI
    } 
    if(rightI < k && map.get(heap[rightI]) < map.get(heap[minIndex])) {
      minIndex = rightI
    }
    
    if(minIndex != i) {
      swap(heap, i, minIndex)
      i = minIndex
    } else {
      break
    }
  }
}

function swap(arr, i, j) {
  let temp = arr[i]
  arr[i] = arr[j]
  arr[j] = temp
}


```

3. 数组中的第K个最大元素

   在未排序的数组中找到第K个最大的元素。你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

   ```javascript
   输入: [3,2,1,5,6,4] 和 k = 2
   输出: 5
   ```

   解法一： 数组排序

   ```javascript
   let findKthLargest = function(nums, k) {
     nums.sort((a, b) => b - a)
     return nums[k-1]
   }
   ```

   解法二:  构造前k个最大元素最小堆, 取堆顶

   - 从数组中取前 `k` 个数（ `0` 到 `k-1` 位），构造一个小顶堆

   - 从 `k` 位开始遍历数组，每一个数据都和小顶堆的堆顶元素进行比较，如果小于堆顶元素，则不做任何处理，继续遍历下一元素；如果大于堆顶元素，则将这个元素替换掉堆顶元素，然后再堆化成一个小顶堆。

   - 遍历完成后，堆顶的数据就是第 K 大的数据

     ```javascript
     let findKthLargest = function(nums, k) {
       let heap = [,], i = 0
       while(i < k) {
         heap.push(nums[i++])
       }
       buildHeap(heap, k)
       for(let i = k; i< nums.length; i++) {
         if(heap[1] < nums[i]) {
           heap[1] = nums[i]
           heapify(heap, k, i)
         }
       }
       return heap[1]
     }
     
     function buildHeap(heap, k) {
       if(k == 1) return
       for(let i = Math.floor(k/2); i>=1; i--) {
         heapify(heap, k, i)
       }
     }
     function heapify(heap, k, i) {
       while(true) {
         let minIndex = i
         const leftI = 2 * i
         const rightI = 2 * i + 1
         if(leftI < k && heap[leftI] < heap[i]) {
           minIndex = leftI
         }
         if(rightI < k && heap[rightI] < heap[minIndex]) {
           minIndex = rightI
         }
         if(minIndex != i) {
           swap(heap, i, minIndex)
           i = minIndex
         } else {
           break;
         }
       }
     }
     function swap(arr, i, j) {
       let temp = arr[i]
       arr[i] = arr[j]
       arr[j] = temp
     }
     ```

     

