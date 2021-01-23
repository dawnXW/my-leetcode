# leetcode386

[题目描述](https://leetcode-cn.com/problems/lexicographical-numbers/)

 方法一，定义一个比较方法，然后merge-sort，或者quick-sort

 方法二，想象成一个树，用dfs遍历每一个节点

 ```python
 class Solution(object):
    def lexicalOrder(self, n):
        """
        :type n: int
        :rtype: List[int]
        """
        res = []
        self.dfs(0, n, res)
        return res

    def dfs(self, base, n, res):
        if base:
            res.append(base)
        for i in xrange(0, 10):
            newBase = base * 10 + i
            if newBase > n:
                break
            if newBase:
                self.dfs(newBase, n, res)
```
