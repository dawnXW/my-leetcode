# leetcode307
[题目描述](https://leetcode-cn.com/problems/range-sum-query-mutable/)
<br>
如果是一个List，不处理，修改一个值是```O(1)```，求和是 ```O(n)```。
```python
class NumArray(object):

    def __init__(self, nums):
        N = len(nums)
        self.tree = [0] * N
        self.tree.extend(nums)

    def update(self, i, val):
        self.nums[i] = val

    def sumRange(self, i, j):
        return sum(self.nums[i:j+1])
```
<br>
<br>
如果是一个List，预存求和，预处理时间是```O(n)```。修改一个值是```O(n)```，求和是```O(1)```。
<br>
<br>
如果是一个线段树，预存求和，预处理时间是```O(n)```。修改一个值是```O(logn)```，求和是```O(logn)```。
<br>
用二叉树可能也可以实现。
