# leetcode396

[题目描述](https://leetcode-cn.com/problems/rotate-function/)

<br>

## Naive 方法（超时）

O(n^2) 的时间复杂度

<br>

```python
class Solution(object):
    def maxRotateFunction(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        N = len(A)
        if not N:
            return 0
        res = -sys.maxint
        for offset in xrange(N):
            tmp = 0
            x = 0
            pos = offset
            res += x * A[pos]
            pos += 1
            x += 1
            if pos == N:
                pos = 0
            while pos != offset:
                tmp += x * A[pos]
                pos += 1
                x += 1
                if pos == N:
                    pos = 0
            res = max(res, tmp)
        return res
```

## 简化运算

O(n) 的时间复杂度

<br>

```python
class Solution(object):
    def maxRotateFunction(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        N = len(A)
        if not N:
            return 0
        sumValue = 0
        left = [0]
        for i in xrange(N):
            sumValue += A[i]
            left.append(sumValue)
        sumValue = 0
        right = [0] * (N+1)
        for i in xrange(N-1, -1, -1):
            sumValue += A[i]
            right[i] = sumValue
        res = 0
        power = 0
        for num in A:
            res += power * num
            power += 1
        tmp = res
        for i in xrange(1, N):
            #print tmp, right[i], left[i-1], (N-1) * A[i-1]
            tmp += -right[i] - left[i-1] + (N-1) * A[i-1]
            res = max(tmp, res)
        return res
```

<br>

优化：left和right可以融合
