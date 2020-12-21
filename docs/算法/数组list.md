1. [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

```javascript
function merge(nums1, m, nums2, n) {
  let length = m + n
  while(n > 0) {
    if(m<=0) {
      nums1[--length] = nums2[--n]
      continue
    }
    nums1[--length] = nums1[m-1] >= nums2[n-1] ? nums1[--m] : nums2[--n]
  }
}
```

2. [两数之和](https://leetcode-cn.com/problems/two-sum/)

   给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

   ```javascript
   function twoSum(nums, target) {
     let map = new Map()
     for(let i = 0; i < nums.length; i++) {
       if(map.has(target - nums[i])) {
         return [map.get(target-nums[i]), i]
       } else {
         map.set(nums[i], i)
       }
     }
     return []
   }
   ```

   3. 三数之和

      + 先排序数组，从最小的元素开始算起
      + 设定好最小元素后, 用双指针法, 一个指针L指向最小元素的后一个元素, 一个指针指向最大元素R
      + 三数之和如果大于0, 则说明R太大， 需要向前走一位, R--. 反之 L太小, L++

      ```javascript
      function threeSum(nums, target) {
        let ans = []
        const len = nums.length
        if(nums == null || len < 3) return ans
        nums.sort()
        for(let i = 0; i < len; i++) {
          if(nums[i] > 0) break; // 当前数字大于0， 则3数之和一定大于0
          if(i > 0 && nums[i] == nums[i-1]) continue; // 去重
          let L = i + i
          let R = len - 1
          while(L < R) {
            const sum = nums[i] + nums[L] + nums[R]
            if(sum == 0) {
              ans.push([nums[i], nums[L], nums[R]])
              while(L < R && nums[L] == nums[L+1]) L++
              while(L < R && nums[R] == nums[R +1]) R--
              L++
              R--
            } else if(sum < 0) {
              L++
            } else if(sum >0) {
              R--
            }
          }
        }
        return ans
      }
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