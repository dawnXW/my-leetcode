# leetcode311
[题目描述](https://leetcode-cn.com/problems/verify-preorder-serialization-of-a-binary-tree/)
<br>
使用dfs做树的前序遍历
```python
class Solution(object):
    def isValidSerialization(self, preorder):
        self.idx = 0
        preorder = preorder.split(',')
        self.N = len(preorder)
        self.preorder = preorder      
        return self.dfs() and self.idx == self.N


    def dfs(self):
        if self.idx >= self.N:
            return False

        value = self.preorder[self.idx]
        self.idx += 1
        if value == '#':
            return True

        # left
        if not self.dfs():
            return False

        # right
        if not self.dfs():
            return False

        return True
```

<br>

计算节点数量即可

```python
class Solution(object):
    def isValidSerialization(self, preorder):
        preorder = preorder.split(',')
        N = len(preorder)
        if not N:
            return True
        stack = 0
        slots = 1
        for val in preorder:
            slots -= 1
            if slots < 0:
                return False
            if val != '#':
                slots += 2
        return slots == 0
```
