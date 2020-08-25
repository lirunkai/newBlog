### 堆

1. [最后一块石头的重量](https://leetcode-cn.com/problems/last-stone-weight/)

```python
class Solution:
  def lastStoneWeight(self, stones: List[int]) -> int:
      while len(stones) > 1:
        stones.sort()
        stones.append(stones.pop() - stones.pop())
      return stones[0]
```

2. [最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

排序解法

```python
class Solution:
  def getLeastNumbers(self, nums: List[int], k:int) -> List[int]:
    nums.sort()
    return nums[:k]
```

最小堆解法
```python
class Solution:
  def getLeastNumbers(self, nums: List[int], k:int) -> List[int]:
    if k == 0:
      return []
    
    hp = [-x for x in nums[:k]]
    heapq.heapify(hp)
    for i in range(k, len(nums)):
      if -hp[0] > nums[i]:
        heapq.heappop(hp)
        heapq.heappush(hp, -arr[i])
    res = [-x for x in hp]
    return res
```

3. [数据流中的第k大数字](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/)

```python
class KthLargest:

  def __init__(self, k: int, nums: List[int]):
     self.k = k
     self.nums = nums
     heapq.heapify(self.nums)
     while len(self.nums) > k:
      heapq.heappop(self.nums)
  
  def add(self, val: int) -> int:
    if len(self.nums) < self.k:
      heapq.heappush(self.nums, val)
    else:
      top = self.nums[0]
      if top < val:
        heapq.heapreplace(self.nums, val)
    return self.nums[0]
```