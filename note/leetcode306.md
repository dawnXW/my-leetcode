# leetcode306
[题目描述](https://leetcode-cn.com/problems/additive-number/)
<br>
DFS的方法遍历所有情况。
<br>
这个其实是回溯问题，DFS的方法与<font color=red>**之前的节点有关**</font>。
<br>
用一个<font color=red>**栈**</font>，记录之前的结果。

```python
class Solution(object):
    def isAdditiveNumber(self, num):
        def backtrack(num, stack):
            res = False
            if not num:
                res = len(stack) >= 3
            else:
                if len(stack) < 2:
                    target = None
                else:
                    target = stack[-1] + stack[-2]

                if num[0] == '0': # 注意判断的类型是char
                    if not target:
                        stack.append(0)
                        res = backtrack(num[1:], stack)
                        stack.pop()
                else:
                    for i in xrange(1, len(num)+1): # 这个地方注意范围，是 len(num)+1)
                        value = int(num[0:i])
                        if not target or value == target:
                            stack.append(value)
                            res = backtrack(num[i:], stack)
                            stack.pop()
                        if res:
                            break
                        if target and value > target:
                            break
            return res

        if backtrack(num, []):
            return True
        return False
```
