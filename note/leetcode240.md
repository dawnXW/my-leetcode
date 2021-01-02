# leetcode240
[题目描述](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)
<br>
核心要从左下角（右上角）出发
```python
class Solution(object):
    def searchMatrix(self, matrix, target):
        m = len(matrix)
        n = len(matrix[0])
        i = m-1
        j = 0
        while i >= 0 and j < n:
            if matrix[i][j] == target:
                return True
            if matrix[i][j] < target:
                j += 1
            else:
                i -= 1
        return False
```
