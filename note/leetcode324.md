# leetcode324
[题目描述](https://leetcode-cn.com/problems/wiggle-sort-ii/)
<br>

如果连续两个数相等怎么办，如果连续多个数相等怎么办。

<br>
正着来不可以。有2n个数时，最多有n个数相等，有2n+1个数时，最多n+1个数相等。需要讨论极端的情况。

```python
class Solution(object):
    def wiggleSort(self, nums):
        nums.sort()
        N = len(nums)
        half = (N+1) // 2
        x = nums[:half]
        y = nums[half:]
        for i in xrange(half):
            nums[2 * i] = x[i]
            if i < len(y):
                nums[2 * i + 1] = y[i]
```

<br>
倒着来可以

```python
class Solution(object):
    def wiggleSort(self, nums):
        nums.sort()
        N = len(nums)
        half = (N+1) // 2
        x = nums[:half]
        y = nums[half:]
        for i in xrange(half):
            nums[2 * i] = x[half-i-1]
            if i < len(y):
                nums[2 * i + 1] = y[len(y)-i-1]
```
