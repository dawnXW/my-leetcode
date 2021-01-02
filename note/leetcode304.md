# leetcode304
[题目描述]()
```python
class NumMatrix(object):

    def __init__(self, matrix):
        if not matrix or not matrix[0]:
            return

        self.valid = True
        self.m = len(matrix)
        self.n = len(matrix[0])

        self.matrix = [[0] * self.n for _ in xrange(self.m)]
        for i in xrange(self.m):
            for j in xrange(self.n):
                x = matrix[i][j]
                if i:
                    x += self.matrix[i-1][j]
                if j:
                    x += self.matrix[i][j-1]
                if i and j:
                    x -= self.matrix[i-1][j-1]
                self.matrix[i][j] = x

    def sumRegion(self, row1, col1, row2, col2):
        if not self.valid \
        or row1 < 0 or row1 >= self.m or row2 < 0 or row2 >= self.m or row1 > row2 \
        or col1 < 0 or col1 >= self.n or col2 < 0 or col2 >= self.n or col1 > col2:
            return None

        ret = self.matrix[row2][col2]
        if row1:
            ret -= self.matrix[row1-1][col2]
        if col1:
            ret -= self.matrix[row2][col1-1]
        if row1 and col1:
            ret += self.matrix[row1-1][col1-1]
        return ret
``````
