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

3. [子域名访问计数](https://leetcode-cn.com/problems/subdomain-visit-count/)

```python
class Solution:
  def subdomainVisits(self, cpdomains: List[str]) -> List[str]:
    cp = collections.Counter()
    for c in cpdomains:
      count, domain = c.split()
      count = int(count)
      args = domain.split('.')
      for i in range(len(args)):
        cp[''.join(args[i:])] += count
      return ['{} {}'.format(v, k) for k, v in cp.items()]
```

4. [“气球” 的最大数量](https://leetcode-cn.com/problems/maximum-number-of-balloons/)

```python
class Solution:
    def maxNumberOfBalloons(self, text: str) -> int:
        return min(text.count(key)//num for key, num in collections.Counter('balloon').items())
```

5. [两句话中的不常见单词](https://leetcode-cn.com/problems/uncommon-words-from-two-sentences/)

```python
class Solution:
    def uncommonFromSentences(self, A: str, B: str) -> List[str]:

        return [ key for key, val in collections.Counter((A + ' ' + B).split()).items() if val == 1]
```

6. [员工的重要性](https://leetcode-cn.com/problems/employee-importance/)

```python
"""
# Definition for Employee.
class Employee:
    def __init__(self, id: int, importance: int, subordinates: List[int]):
        self.id = id
        self.importance = importance
        self.subordinates = subordinates
"""
class Solution:
  def getImportance(self, employees: List['Employee'], id: int) -> int:
    dic = { em.id: em for em in employees}
    def dfs(depId):
      employ = dic[depId]
      return employ.importance + sum(dfs(x) for x in employ.subordinates)
    return dfs(id)
```

7. [实现一个哈希表](https://leetcode-cn.com/problems/design-hashmap/submissions/)

思路： 

1. 通过哈希队列存储
2. 处理哈希冲突

```python

```

8. [两个列表的最小索引总和](https://leetcode-cn.com/problems/minimum-index-sum-of-two-lists/)

思路：

直接上哈希

```python
class Solution:
  def findRestaurant(self, num1: List[str], num2: List[str]) -> List[str]:
    k = 2 ** 32 
    dic = {}
    if len(list1) < len(list2):
      list1, list2 = list2, list1
    for i in range(len(list1)):
      dic[list[i]] = i
    for j in range(len(list2)):
      val = dic.get(list2[j])
      if val is not None:
        if val + j < k:
          k = val + j
          res = []
          res.append(list2[j])
        elif val + j == k:
          res.append(list2[j])
    return res
```

9. [猜数字游戏](https://leetcode-cn.com/problems/bulls-and-cows/)

思路:

先找出所有公牛

在找出所有母牛

```python
class Solution:
  def getHint(self, num1: List[int], num2: List[int]) -> str:
    count1 = count2 = 0
    for i in range(len(num1)):
      if num1[i] == num2[i]:
        count1 += 1
    
    dic1 = collections.Counter(num1)
    dic2 = collections.Counter(num2)

    for k in dic1:
      if k in dic2:
        count2 += min(dic1[k], dic2[k])
      
    count2 = count2 - count1

    return '{}A{}B'.format(count1, count2)
```



10. [同构字符串](https://leetcode-cn.com/problems/isomorphic-strings/)

思路: 通过分类来标示出两个数组 比如`add` 标示出[1, 2, 2], `adde` 标示出`[1, 2, 2, 3]`

```python
class Solution:
  def isIsomorphic(self, s: str, t: str) -> bool:
    dic = {}
    s_list = []
    new = 1
    for i in s:
      if i in dic:
        s_list.append(dic[i])
      else:
        dic[i] = new
        s_list.append(dic[i])
        new += 1

    dic = {}
    t_list = []
    new = 1
    for i in t:
      if i in dic:
        t_list.append(dic[i])
      else:
        dic[i] = new
        t_list.append(dic[i])
        new += 1
    
    returm s_list == t_list
    
```

