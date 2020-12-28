# leetcode213
[题目内容](https://leetcode-cn.com/problems/house-robber-ii/)
<br>
这应该是一道动态规划的题目
<br>
一个数组求和，要求不能取连续的2个数，得到求和的最大值。
<br>
假设数组长```N```，```1 < n < N```，包含```n```的最大值为```X(n)```，不包含```n```的最大值为```Y(n)```<br>
前```n```个数求和的最大值为```max(X(n-1), Y(n-1)+value(n))```。
<br><br>
<font color=red>注意1: 这个题目中所有的房子围城了一圈。<br></font>
需要我们单独讨论```n=0```和```n=N```两种情况。

<br>
<font color=red>注意2: dp的写法。下面是一个错误的示范</font>

```python
def dp(self, nums):
    N = len(nums)
    if N < 1:
        return 0
    X = nums[0] # included
    Y = 0 # not included
    res = max(X, Y)
    for i in range(1, N):
        newX = Y + nums[i]
        newY = X # 错误！！！
        res = max(Y, X)
        Y = newY
        X = newX
    return res
```

<br>
最终代码

```python
class Solution(object):
    def rob(self, nums):
        N = len(nums)
        if N == 0:
            return 0
        if N == 1:
            return nums[0]
        if N == 2:
            return max(nums[0], nums[1])
        # include nums[0]
        res1 = nums[0] + self.dp(nums[2:N-1])

        # not include nums[0]
        res2 = self.dp(nums[1:])

        return max(res1, res2)

    def dp(self, nums):
        N = len(nums)
        if N < 1:
            return 0
        X = nums[0] # included
        Y = 0 # not included
        res = max(X, Y)
        for i in range(1, N):
            newX = Y + nums[i]
            newY = max(X, Y)
            Y = newY
            X = newX
            res = max(Y, X)
        return res
```

<br>
标准答案

```python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        def rob1(nums):
            yes, no = 0,0
            for i in nums:
                no, yes = max(yes, no), no+i
            return max(no, yes)
        return max(rob1(nums[len(nums)!=1:]), rob1(nums[:-1]))
```
