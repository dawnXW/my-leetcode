# leetcode400

[题目描述](https://leetcode-cn.com/problems/nth-digit/)

代码+手写的测试case

```python
class Solution(object):
    def findNthDigit(self, n):
        """
        :type n: int
        :rtype: int
        """
        # Test: n = 500
        posCnt = 0
        prevCnt = 0
        prevNum = 0
        deltaCnt = 0
        deltaNum = 0
        # 9 90*2 900* 3
        # 1 ~ 9  1 ~ 9
        # 10 ~ 189  10 ~ 99
        # 190 ~ 2889  100 ~ 999
        while n > prevCnt + deltaCnt: # 500,0 500,9 500,189 500,2889
            prevCnt += deltaCnt # 0 9 189
            prevNum += deltaNum # 0 9 99
            posCnt += 1 # 1 2 3
            deltaNum = 9 * pow(10, posCnt-1) # 9 90 900
            deltaCnt = posCnt * deltaNum # 9 180 2700
        num = prevNum + (n - prevCnt) / posCnt # 99+(500-189)/3=202
        offset = (n - prevCnt) % posCnt # (500-189)%3=2
        if offset > 0:
            num += 1 # 203
            cnt = posCnt - offset # 1
            while cnt:
                num /= 10 # 20
                cnt -= 1 # 0
        return num % 10 # 0
```
