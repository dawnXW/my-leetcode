# leetcode241
[题目描述](https://github.com/dawnXW/my-leetcode.git)
<br>
~~全排列问题，用回溯/DFS的方法解决。~~
<br>
分冶算法+dp
```python
class Solution(object):

    operator = ['+', '-', '*']
    dpTable = {}

    def diffWaysToCompute(self, input):
        """
        :type input: str
        :rtype: List[int]
        """
        if self.dpTable.has_key(input):
            return self.dpTable[input]
        N = len(input)

        res = []
        for i in range(N):
            if input[i] in self.operator:
                left = self.diffWaysToCompute(input[:i])
                right = self.diffWaysToCompute(input[i+1:])

                for x in left:
                    for y in right:
                        if input[i] == '+':
                            res.append(x+y)
                        elif input[i] == '-':
                            res.append(x-y)
                        else:
                            res.append(x*y)                    

        if len(res) == 0:
            res.append(int(input))

        self.dpTable[input] = res

        return res
```
