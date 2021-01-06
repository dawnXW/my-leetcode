# leetcode337
[题目描述](https://leetcode-cn.com/problems/house-robber-iii/)
<br>
通过回溯可以遍历所有情况，然后选出最大值，所有情况可能有```O(2^n)```种，显然不可能。
<br>
题目中要求不能连续抢劫，如果可以连续，就是**贪心算法**，如果不能，就需要**贪心算法 + 动态规划**

```python
class Solution(object):
    def rob(self, root):
        # A included
        # B not included
        def dfs(node):
            if not node:
                return 0, 0
            left_A, left_B = dfs(node.left)
            right_A, right_B = dfs(node.right)
            A = node.val + left_B + right_B
            B = max(left_A, left_B) + max(right_A, right_B)
            return A, B

        A, B = dfs(root)

        return max(A, B)
```
