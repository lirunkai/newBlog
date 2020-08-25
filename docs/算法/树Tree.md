
### 树

最顶极节点称为 根节点

完全二叉树： 每个节点都有两个子节点

```python
class TreeNode:
  def __init__(self, val):
    self.val = val
    self.left, self.right = None, None
```

二叉搜索树:

1. 左子树上所有结点的值均小于它的根结点的值

2. 右子树上所有结点的值均大于它的根结点的值

特殊情况下的二叉搜索树：

子节点都在左子树， 子节点都在右子树， 查找的时间复杂度退化为 O（n）

为了解决这个问题 出现了红黑树

树的三种遍历

1. 前序遍历 Pre-order 根 - 左 - 右

```python
def preorder(self, root):
  if root:
    self.traverse_path.append(root.val)
    self.preorder(root.left)
    self.preorder(root.right)
```

2. 中序遍历 In-order 左 - 根 - 右

```python
def inorder(self, root):
  if root:
    self.inorder(root.left)
    self.traverse_path.append(root.val)
    self.inorder(root.right)
```

3. 后序遍历 Post-order 左 - 右 - 根

```python
def postorder(self, root):
  if root:
    self.postorder(root.left)
    self.postorder(root.right)
    self.traverse_path.append(root.val)
```

1. 验证二叉搜索树

```python

def helper(self, root):
  if root is None:
    return True
  if not self.helper(root.left):
    return False
  if not self.helper(root.right)

```

2. 二叉树最近公共祖先

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

3. N叉树的前序遍历

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

4. 验证二叉搜索树

一个二叉搜索树具有如下特征：
  节点的左子树只包含小于当前节点的数。
  节点的右子树只包含大于当前节点的数。
  所有左子树和右子树自身必须也是二叉搜索树。

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

5. 二叉树的最大深度

```python
class Solution:
  def maxDeepCount(self, root: TreeNode) -> int:
    if not root:
      return 0
    
    return max(self.maxDeepCount(root.left), self.maxDeepCOunt(root.right)) + 1
```

6. 二叉树的最小深度

深度优先解法
```python
class Solution:
  def minDepth(self, root: TreeNode) -> int:
    if not root:
      return 0
    
    if not root.left and not root.right:
      return 1
    
    min_depth = 10**9
    if root.left:
      min_depth = min(self.minDepth(root.left), min_depth)
    if root.right:
      min_depth = min(self.minDepth(root.right), min_depth)

    return min_depth + 1
```

广度优先
```python
class Solution:
  def minDepth(self, root: TreeNode) -> int:
    if not root:
      return 0
    
    que = collecions.deque([(root, 1)])
    
    while que:
      node, depth = que.popleft()

      if not node.left and not node.right:
        return depth
      
      if node.left:
        que.append((node.left, depth + 1))
      if node.right:
        que.append((node.right, depth + 1))
      
    return 0
```