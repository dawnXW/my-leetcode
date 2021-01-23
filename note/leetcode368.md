# leetcode368

[题目描述](https://leetcode-cn.com/problems/largest-divisible-subset/)

<br>

```python
class Solution(object):
    def largestDivisibleSubset(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        N = len(nums)
        nums.sort()
        factors = [[] for _ in xrange(N)]
        for idx in xrange(1, N):
            num = nums[idx]
            for i in xrange(idx):
                val = nums[i]
                if num % val == 0:
                    factors[idx].append(i)
        lastIdx = 0
        maxCnt = 1
        prevList = [-1]
        dp = [1]
        for idx in xrange(1, N):
            cnt = 1
            prev = -1
            for factorIdx in factors[idx]:
                if dp[factorIdx] >= cnt:
                    cnt = dp[factorIdx] + 1
                    prev = factorIdx
            dp.append(cnt)
            prevList.append(prev)
            if cnt > maxCnt:
                maxCnt = cnt
                lastIdx = idx
        res = []
        while lastIdx != -1:
            res.append(nums[lastIdx])
            lastIdx = prevList[lastIdx]
        res.reverse()
        return res
```

这个题目感觉是一个缝合怪，需要用到很多做题的思路
- 需要求公因数
- 需要对数组排序
- 需要用到dp，记录之前的结果
- 同时需要找到最大值的路径，复原返回
