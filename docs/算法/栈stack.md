1. [删除最外层的括号](https://leetcode-cn.com/problems/remove-outermost-parentheses/submissions/)

思路: 

遇到左括号入栈， 入栈后大与1， 说明有外层包裹
遇到右括号出栈， 出栈后大于0， 说明有外层包裹

```python
class Solution:
  removeOuterParentheses(self, S:str) -> str:
    stack, result = [], ''
    for k in S:
      if k == '(':
        stack.append(k)
        if len(stack) > 1:
          result += '('
      else:
        stack.pop()
        if len(stack) > 0:
          result += ')'
    return result
```

2. [用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

思路:

1. 创建一个输入栈， 一个输出栈
2. 添加元素时，先添加进输入栈
3. 删除元素时，看输出栈是否为空？不为空直接输出，为空则将输入栈的数据全部出栈进入输出栈再输出

```python
class CQueue:

  def __init__(self):
    self.in_stack = []
    self.out_stack = []
  
  def appendTail(self, value:int) -> None:
    self.in_stack.append(value)
  
  def deleteHead(self) -> int:
    if self.out_stack:
      return self.out_stack.pop()
    else:
      if self.in_stack:
        while self.in_stack:
          self.out_stack.append(self.in_stack.pop())
        return self.out_stack.pop()
      else:
        return -1

```

3. [删除字符串中的所有相邻重复项](https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/)

思路:
1. 设一个栈，每次入栈进行判断，如果上一个元素与当前元素一致， 则出栈

```python
class Solution:
  def removeDuplicates(self, S:str) -> str:
    stack = []
    for k in S:
      if stack and stack[-1] == k:
        stack.pop()
      else:
        stack.append(k)
    return ''.join(stack)
```

4. [棒球比赛](https://leetcode-cn.com/problems/baseball-game/submissions/)

给定一个字符串列表，每个字符串可以是以下四种类型之一：
1.整数（一轮的得分）：直接表示您在本轮中获得的积分数。
2. "+"（一轮的得分）：表示本轮获得的得分是前两轮有效 回合得分的总和。
3. "D"（一轮的得分）：表示本轮获得的得分是前一轮有效 回合得分的两倍。
4. "C"（一个操作，这不是一个回合的分数）：表示您获得的最后一个有效 回合的分数是无效的，应该被移除。

思路: 存储的是成绩， 而不是每次的比分

```python
class Solution:
  def calPoints(self, opts: List[str]) -> int:
    res, stack = 0, []
    for k in opts:
      if k == 'C':
        stack.pop()
      elif k == 'D':
        stack.append(stack[-1] * 2)
        res += stack[-1]
      elif k == '+':
        stack.append(stack[-1] + stack[-2])
        res += stack[-1]
      else:
        stack.append(int(k))
        res += stack[-1]
    return res
```

5. 用队列实现栈

```python
from collections import deque
class MyStack:
  def __init__(self) {
    self.data = deque()
    self.help = deque()
  }

  def push(self, x:int) -> None:
    self.data.append(x)
  
  def pop(self) -> int:
    while len(self.data) > 1:
      self.help.append(self.data.popleft())
    temp = self.data.popleft()
    self.help, self.data = self.data, self.help
    return temp

  def top(self) -> int:
    while len(self.data) >1:
      self.help.append(self.data.popleft())
    temp = self.data.popleft()
    self.help.append(temp)
    self.help, self.data = self.data, self.help
    return temp
  
  def isEmpty(self) -> bool:
    return not bool(self.data)
```

6. [下一个更大元素](https://leetcode-cn.com/problems/next-greater-element-i/)

思路: 

1. 求nums2中每个元素的下一个的最大值，并存储到字典中
2. num1直接读取字典中的值

```python
class Solution:
  def nextGeneratorElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
    stack, hashmap = [], dict()
    for k in nums2:
      while stack and stack[-1] < k:
        hashmap[stack.pop()] = k
      stack.append(k)
    return [hashmap.get(key, -1) for key in nums1]
```

7. [用栈操作构建数组](https://leetcode-cn.com/problems/build-an-array-with-stack-operations/)

思路:

一共就两种操作: 
1. 匹配 `Push`
2. 不匹配 `Push Pop`

```python
class Solution:
  def buildArray(self, target: List[int], n: int) -> List[str]:
      stack, j = [], 0
      if not target:
          return []
      for k in range(1, target[-1]+1): # 不使用n作为最终节点， target[-1]是循环遍历最大的值了
        if k == target[j]:
          stack.append('Push')
          #target.pop(0) # pop0会造成之后target元素的移动
          j += 1
        else:
          stack.extend(['Push', 'Pop'])
      
      return stack
```

8. [栈的最小值](https://leetcode-cn.com/problems/min-stack-lcci/)

思路:

1. 一个栈来存储输入的值
2. 一个栈来存储len的min值

```python
class MinStack:
  def __init__(self) {
    self.stack = []
    self.min_stack = []
  }

  def push(self, x:int) -> None:
    self.stack.append(x)
        if not self.min_stack or self.getMin() >= x:
            self.min_stack.append(x)
  
  def pop(self) -> None:
    if self.stack.pop() == self.getMin():
            self.min_stack.pop()

  def top(self) -> int:
    return self.stack[-1]

  def getMin(self) -> int:
    return self.min_stack[-1]
```

9. [比较含退格的字符串](https://leetcode-cn.com/problems/backspace-string-compare/)

```python
class Solution:
  def backspaceCompare(self, S:str, T:str) -> bool:
    s_stack = []
    t_stack = []
    for i in S:
      if i == '#':
        if s_stack:
          s_stack.pop()
      else:
        s_stack.append(i)
    for j in T:
      if j == '#':
        if t_stack:
          t_stack.pop()
      else:
        t_stack.append(j)

    s = ''.join(s_stack)
    t = ''.join(t_stack)

    return s == t
```

10. [整理字符串](https://leetcode-cn.com/problems/make-the-string-great/)

思路: 遇到大小写一起的 直接删

```python
class Solution:
  def makeGood(self, s: str) -> str:
    stack = []

    for k in s:
      if stack and stack[-1].lower() == k.lower() and k != stack[-1]:
        stack.pop()
      else:
        stack.append(k)

    return ''.join(stack)
```

11. [简单的括号](https://leetcode-cn.com/problems/valid-parentheses/submissions/)

```python
class Solution:
  def isValid(self, s:str) -> bool:
    dic = { '(': ')', '{': '}', '[': ']', '?': '?'}
    stack = ['?']
    for k in s:
      if k in dic:
        stack.append(k)
      elif dic[stack.pop()] != k: 
        return False
    return len(stack) == 1
```