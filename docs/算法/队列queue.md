**队列**

先入先出

使用： 循环队列， 阻塞队列， 并发队列， 排队请求

实现：

基于数组实现的是顺序队列

基于链表实现的是链式队列

循环队列实现时需要注意： 确定好空队列和队满的判定情况

1. 滑动窗口的最大值

给一个k，求nums列表中

思路：
1. 需要双端队列， 队首永远保持k范围内最大数
2. 判断最大值是否在新的k范围内 
```python
class Solution:
  def maxSlidingWindow(self, nums:List[int], k:int) -> List[int]:
    deque = collections.deque()
    res, n = [], len(n)

    for i, j in zip(range(i - k, n+1-k), range(n)):
      if i > 0 and deque[0] == nums[i - 1]:
        deque.popleft()
      while deque and deque[-1] < nums[j]:
        deque.pop()
      deque.append(nums[j])
      if i >0:
        res.append(deque[0])
```