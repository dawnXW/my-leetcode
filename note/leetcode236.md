# leecode236
[题目内容](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)
<br>
题目给出的是一个树的root<br>
如果把树铺程一个List，那么根据p和q的index就可以找到p和q的公共最深的root<br>
在评论中发现，这其实是[**最近公共祖先（Least Common Ancestors，LCA）问题**](https://blog.csdn.net/ywcpig/article/details/52336496)

**naive解法**，耗时84ms
```python
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        if root == None:
            return root
        if root.val == p.val or root.val == q.val:
            return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left != None and right != None:
            return root
        if left != None:
            return left
        if right != None:
            return right
        return None
```
<br>

发现如果**减少**一次```if```判断，可以减少耗时到60ms<br>
```if```语句和语句中总的句柄的数量有关，和```if```的数量无关
```python
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        if root == None:
            return root
        if root.val == p.val or root.val == q.val:
            return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left != None and right != None:
            return root
        if left != None:
            return left
        return right
```
<br>

把结果**记在**一个```self```的变量里，测试结果并没有提升<br>
但是要注意，如果```q```是```p```的父系节点，返回值是```q```
```python
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        self.res = root
        def dfs(node, p, q):
            if node == None:
                return False
            equal = False
            if node.val == p or node.val == q:
                equal = True
            left = dfs(node.left, p, q)
            right = dfs(node.right, p, q)
            # print node.val, equal, left, right
            if (left and right) or (equal and (left or right)):
                self.res = node
                return False
            return left or right or equal
        dfs(root, p.val, q.val)
        return self.res
```
