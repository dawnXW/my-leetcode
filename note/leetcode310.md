# leetcode310
[题目描述](https://leetcode-cn.com/problems/minimum-height-trees/)
<br>
题目的要求，是给n个点，求里面的一个点，这个点到所有点的距离的最大值最小，求这个最小值。
<br>
假设点的集合为```p0, p1, p2, ...```
<br>
```
result = min(max(p0px)(x<>0), max(p1px)(x<>1), max(p2px)(x<>2), ...)
```

所以暴力穷举法是可以满足的。遍历每个点，求最大值，再求最小值，如果用O(1)的时间可以得到与任意点的距离，时间复杂度是```O(n^2)```

<br>

现在的问题是：**是否可以优化这个算法？**
<br>
找到最长的2个点的距离然后除以2? <font color=red>可以</font>

<br>
如何找到最长的2个点的距离？<font color=red>拓扑排序</font>

```python
class Solution(object):
    def findMinHeightTrees(self, n, edges):
        connections = [set() for _ in range(n)]
        for edge in edges:
            a = edge[0]
            b = edge[1]
            connections[a].add(b)
            connections[b].add(a)

        # bfs tuopu
        pointSet = set()
        while len(pointSet) < n:
            tmpSet = set()
            for i in xrange(n):
                if i not in pointSet and len(connections[i]) <= 1:
                    tmpSet.add(i)
                    pointSet.add(i)
            for a in tmpSet:
                if connections[a]:
                    b = connections[a].pop()
                    connections[b].remove(a)
        return list(tmpSet)
```

如何优化性能？
