# leetcode389
[题目内容](https://leetcode-cn.com/problems/find-the-difference/)
<br>
***方法一*** 对char array转int再求和。leetcode显示12ms。
```python
class Solution(object):
    def findTheDifference(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        res = 0
        for c in t:
            res += ord(c)
        for c in s:
            res -= ord(c)
        return chr(res)
```
***方法二*** 使用count，统计string中每一个substring（char）出现的次数。与方法一耗时接近。<br>
也可以用一个List来做临时存储，但是性能不如直接count。
```python
str.count(substr)
```
***方法三*** xor。<br>
```python
class Solution(object):
    def findTheDifference(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        res = 0
        for c in s:
            res ^= ord(c)
        for c in t:
            res ^= ord(c)
        return chr(res)
```
与方法一思路类似，但是实际性能不如方法一。<br>
