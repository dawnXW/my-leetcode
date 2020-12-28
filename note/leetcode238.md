# leetcode238
[题目描述](https://leetcode-cn.com/problems/product-of-array-except-self/)
<br>
应该也是动态规划的题目。```output[i]```等于```left * right```。
```python
class Solution(object):
    def productExceptSelf(self, nums):
        N = len(nums)
        left = 1
        output = [0] * N
        for i in range(0, N):
            output[i] = left
            left *= nums[i]
        right = 1
        for i in range(N-1, -1, -1):
            output[i] *= right
            right *= nums[i]
        return output
```
