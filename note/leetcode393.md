# leetcode393

[题目描述](https://leetcode-cn.com/problems/utf-8-validation/)

<br>

可以把二进制的数转换成数字

<br>

这道题需要做很多条件判断，<font color=red>**如何写完代码，检验自己写的逻辑是否正确？**</font>

<br>

可能的方法

- 读自己的代码，回想一下自己为什么这样写?

- 想一些这样写的逻辑是否正确，重复自己的思路（正面验证）

- 提一些case，黑盒验证（实现比较麻烦）

```python
class Solution(object):
    def validUtf8(self, data):
        """
        :type data: List[int]
        :rtype: bool
        """
        # 0xxxxxxx 0~127
        # 110xxxxx 192~223
        # 1110xxxx 224~239
        # 11110xxx 240~247
        # 10xxxxxx 128~191
        cnt = 0
        for num in data:
            numType = self.check(num)
            if numType == -2 \
            or (cnt == 0 and numType < 0) \
            or (cnt > 0 and numType > 0):
                return False
            cnt += numType
        return cnt == 0

    def check(self, num):
        if num < 128:
            return 0
        elif num < 192:
            return -1
        elif num < 224:
            return 1
        elif num < 240:
            return 2
        elif num < 248:
            return 3
        else:
            return -2 # > 247有问题
```
