# leetcode230
[题目描述](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)
## DFS + 递归
```python
class Solution(object):
    def kthSmallest(self, root, k):
        self.cnt = 0
        self.k = k
        self.val = None
        self.dfs(root)
        return self.val

    def dfs(self, node):
        if node.left:
            self.dfs(node.left)
        self.cnt += 1
        if self.cnt == self.k:
            self.val = node.val
            return
        if node.right:
            self.dfs(node.right)
```
<br>

```yield```方法

```python
class Solution(object):
    def kthSmallest(self, root, k):
        def dfs(node):
            if node:
                for x in dfs(node.left):
                    yield x
                yield node.val
                for x in dfs(node.right):
                    yield x

        it = dfs(root)
        for _ in xrange(k):
            ans = next(it)
        return ans
```
