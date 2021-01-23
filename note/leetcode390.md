# leetcode390

[题目描述](https://leetcode-cn.com/problems/elimination-game/)

<br>

数学问题，表述一个递推公式，理论可以 O(1) 解决？

```python
class Solution(object):
    def lastRemaining(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 1:
            return 1
        return 2 * (n/2+1 - self.lastRemaining(n/2))
```
