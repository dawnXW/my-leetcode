# leetcode365

[题目描述](https://leetcode-cn.com/problems/water-and-jug-problem/)

<br>

转换成求最大公约数的问题，x和y的最大公约数如果可以整除z，就可以实现

<br>

更相减损术

<br>

```python
class Solution(object):
    def canMeasureWater(self, x, y, z):
        """
        :type x: int
        :type y: int
        :type z: int
        :rtype: bool
        """
        if z == 0:
            return True
        if x+y < z:
            return False
        if x == 0 and y == 0:
            return False
        if x == 0:
            gcd = y
        elif y == 0:
            gcd = x
        else:
            gcd = self.find(x, y)
        return z % gcd == 0

    def find(self, x, y):
        if x == y:
            return x
        if x == 1 or y == 1:
            return 1
        if x < y:
            x,y = y,x
        return self.find(x-y, y)
```
