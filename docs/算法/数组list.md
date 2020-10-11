1. [有多少小于当前数字的数字](https://leetcode-cn.com/problems/how-many-numbers-are-smaller-than-the-current-number/)

解法一: 暴力搜索
```python
class Solution:
    def smallerNumbersThanCurrent(self, nums: List[int]) -> List[int]:
        dic = dict()
        for i in nums:
            if not i in dic:
                dic[i] = 0
                for j in nums:
                    if j < i:
                        dic[i] += 1
        return [dic[k] for k in nums]
```

优化解法一:
```python
class Solution:
    def smallerNumbersThanCurrent(self, nums: List[int]) -> List[int]:
        n = len(nums)
        vec = [0] * n
        for i in range(n):
            vec[i] = sum(1 for j in range(n) if nums[j] < nums[i])
        return vec
```

解法二: 
增加一个list来统计number按大小出现的次数
增加一个返回数组来取list中处理完的数据
```python
class Solution:
  def smllerNumbersThanCurrent(self, nums: List[int]) -> List[int]:
    n = len(nums)
    cnt, vec = [0] * 101, [0] * n
    for num in nums:
      cnt[num] += 1
    for ct in range(1, 101):
      cnt[ct] += cnt[ct-1]
    for i in range(len(nums)):
      if nums[i]:
        vec[i] = cnt[nums[i] - 1]
    return vec
```

2. [两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

```python
class Solution:
  def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
    set1 = set(nums1)
    set2 = set(nums2)

    if len(set1) > len(set2):
      return [x for x in set1 if x in set2]
    else:
      return [x for x in set2 if x in set1]
```

3. [只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

```python
class Solution:
  def singleNumber(self, nums: List[int]) -> int:
    return sum(set(nums))*2 - sum(nums)
```

4. [分糖果](https://leetcode-cn.com/problems/distribute-candies/)

思路:

如果种类比糖果的一半多，返回种类
如果种类比糖果的一半少， 返回糖果的一半

```python
class Solution:
  def distributeCandies(self, candies: List[int]) -> int:
    category = len(set(candies))
    half = len(candies)//2
    if category < half:
      return int(half)
    else:
      return category
```

5. [第 k 个缺失的正整数](https://leetcode-cn.com/problems/kth-missing-positive-number/)

思路：

1. 预置一个正整数排列数组
2. 没有排列的位置为n

```python
class Solution:
  def findKthPosition(self, arr:List[int], k:int) -> int:
    arrBuf = [0] * 2001
    for i in arr:
      arrBuf[i] = i
    res = 0
    for i in range(1, len(arrBuf)):
      if arrBuf[i] == 0:
        res += 1
      if res == k:
        return i
```


矩形数组

1. [岛屿的周长](https://leetcode-cn.com/problems/island-perimeter/)

思路:

由于岛屿中间没有湖泊，所以岛屿的周长=(长+宽)*2

```python
class Solution:
  def islandPerimeter(self, grid: List[List[int]]) -> int:
    height = len(grid)
    width = len(grid[0])
    res = 0
    for i in range(height):
      for j in range(width):
        if grid[i][j] == 1:
          if j == 0 or grid[i][j - 1] == 0:
            res += 1
          if i == 0 or grid[i-1][j] == 0:
            res += 1
    return res * 2
```