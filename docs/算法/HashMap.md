## HashMap

1. [好数对的数目](https://leetcode-cn.com/problems/number-of-good-pairs/)

傻循环
```python
class Solution:
  def numIdenticalPairs(self, nums: List[int]) -> int:
    res = 0
    for i in range(nums):
      for j in range(i+1, nums):
        if nums[i] == nums[j]:
          res += 1
    return res
```

hashMap
```python
class Solution:
  def numIdenticalPairs(self, nums: List[int]) -> int:
    m = collections.Counter(nums)
    return sum(v*(v-1)//2 for k, v in m.items())
```

2. [宝石与石头](https://leetcode-cn.com/problems/jewels-and-stones/submissions/)

```python
class Solution:
    def numJewelsInStones(self, J: str, S: str) -> int:
        dic = dict()
        for s in S:
            if s in dic:
                dic[s] += 1
            else:
                dic[s] = 1
        res = 0
        for j in J:
            if j in dic:
                res += dic[j]
        return res
```