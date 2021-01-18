# leetcode341
[题目描述](https://leetcode-cn.com/problems/flatten-nested-list-iterator/)

```python
# """
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# """
#class NestedInteger(object):
#    def isInteger(self):
#        """
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        :rtype bool
#        """
#
#    def getInteger(self):
#        """
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        :rtype int
#        """
#
#    def getList(self):
#        """
#        @return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        :rtype List[NestedInteger]
#        """

class NestedIterator(object):

    def __init__(self, nestedList):
        """
        Initialize your data structure here.
        :type nestedList: List[NestedInteger]
        """
        self.flatList = []
        self.getFlatList(nestedList)
        self.idx = 0
        self.length = len(self.flatList)

    def getFlatList(self, nestedList):
        for nestedInteger in nestedList:
            if nestedInteger.isInteger():
                self.flatList.append(nestedInteger.getInteger())
            else:
                self.getFlatList(nestedInteger.getList())


    def next(self):
        """
        :rtype: int
        """
        self.idx += 1
        if self.idx <= self.length:
            return self.flatList[self.idx-1]
        else:
            return None


    def hasNext(self):
        """
        :rtype: bool
        """
        return self.idx < self.length


# Your NestedIterator object will be instantiated and called as such:
# i, v = NestedIterator(nestedList), []
# while i.hasNext(): v.append(i.next())
```
