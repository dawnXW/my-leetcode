# leetcode372

[题目描述](https://leetcode-cn.com/problems/super-pow/)

<br>

分冶算法（<font color=red>超时</font>）

<br>

```python
# 分冶算法
class Solution(object):
    def superPow(self, a, b):
        """
        :type a: int
        :type b: List[int]
        :rtype: int
        """
        dp = {}
        dp["0"] = 1
        dp["1"] = a % 1337
        return self._superPow(dp, a, b)

    def _superPow(self, dp, a, b):
        key = ''.join([str(num) for num in b])
        if dp.has_key(key):
            return dp[key] #dp
        c = 0
        half_b = []
        for num in b:
            half_num = (c*10+num) >> 1
            c = num & 1
            if not half_b and not half_num:
                continue
            half_b.append(half_num)
        res = pow(self._superPow(dp, a, half_b),2) * dp[str(c)] % 1337
        dp[key] = res
        return res
```

<br>

需要用数论中的欧拉算法
