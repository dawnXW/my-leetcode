# leetcode222
[题目描述](https://leetcode-cn.com/problems/count-complete-tree-nodes/)
<br>
题目中是<font color=red>完全二叉树</font>，所以可以有更多的方法
## DFS
略
## Divide And Conquer
```python
class Solution(object):
    def countNodes(self, root):
        if root == None:
            return 0
        lc = self.findLeftLevel(root.left)
        rc = self.findLeftLevel(root.right)

        if lc == rc:
            return (1 << lc) + self.countNodes(root.right)
        else:
            return self.countNodes(root.left) + (1 << rc)

    def findLeftLevel(self, root):
        if root == None:
            return 0
        return 1 + self.findLeftLevel(root.left)
```
