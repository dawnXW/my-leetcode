# leetcode103
[题目内容](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)<br>
看上去是一个BFS的题目<br>
看了评论，发现DFS也可以（差不多）<br>
二叉树的问题，与leetcode17全排列的问题也有一点联系，都是DFS/BFS遍历问题。<br>
下面是一个DFS的方法<br>
```python
class Solution:
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        def dfsBTN(node, res, level):
            if len(res) < level:
                res.append([])
            res[level-1].append(node.val)
            if node.left != None:
                dfsBTN(node.left, res, level+1)
            if node.right != None:
                dfsBTN(node.right, res, level+1)

        res = []
        if root == None:
            return res
        dfsBTN(root, res, 1)
        for i in range(len(res)):
            if i & 1 == 0:
                continue
            res[i].reverse()
        return res
```
这个问题要求锯齿遍历，其实就是奇数行要翻转，这个抽象很棒，所以我用了这个DFS的方法。
