# leetcode207
[题目内容](https://leetcode-cn.com/problems/course-schedule/)
<br>
构造一个非连接的有向图，判断这个图形有没有<B><font color=green>环</font></B>。
<br>
应该有三种方法
<br>
**拓扑排序**152ms
```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        childToParent, parentToChild = self.buildGraph(numCourses, prerequisites)
        recordSet = set()
        while True:
            cnt = 0
            for i in range(numCourses):
                if i not in recordSet and len(childToParent[i]) == 0:
                    for child in parentToChild[i]:
                        childToParent[child].discard(i)
                    recordSet.add(i)
                    cnt += 1
            if cnt > 0:
                continue
            return numCourses == len(recordSet)
        return True

    def buildGraph(self, numCourses, prerequisites):
        childToParent = [set() for _ in range(numCourses)]
        parentToChild = [set() for _ in range(numCourses)]
        for relation in prerequisites:
            parent = relation[0]
            child = relation[1]
            childToParent[child].add(parent)
            parentToChild[parent].add(child)
        return childToParent, parentToChild
```
<br>

**BFS+拓扑**32ms
```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        childToParent, parentToChild = self.buildGraph(numCourses, prerequisites)
        childToParent = [len(x) for x in childToParent]
        checkedNum = 0
        checkedList = []
        for i in range(numCourses):
            if childToParent[i] == 0:
                checkedList.append(i)
        while len(checkedList) != 0:
            x = checkedList.pop()
            checkedNum += 1
            for y in parentToChild[x]:
                childToParent[y] -= 1
                if childToParent[y] == 0:
                    checkedList.append(y)
        return checkedNum == numCourses

    def buildGraph(self, numCourses, prerequisites):
        childToParent = [set() for _ in range(numCourses)]
        parentToChild = [set() for _ in range(numCourses)]
        for relation in prerequisites:
            parent = relation[0]
            child = relation[1]
            childToParent[child].add(parent)
            parentToChild[parent].add(child)
        return childToParent, parentToChild
```

<br>

**DFS**28ms
```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        childToParent, parentToChild = self.buildGraph(numCourses, prerequisites)
        checkedSet = set()
        for relation in prerequisites:
            parent = relation[0]
            visitedSet = set()
            if not self.dfs(parentToChild, parent, checkedSet, visitedSet):
                return False
        return True

    def dfs(self, parentToChild, node, checkedSet, visitedSet):
        if node in visitedSet:
            return False
        if node in checkedSet:
            return True
        checkedSet.add(node)
        visitedSet.add(node)
        for nextNode in parentToChild[node]:
            if not self.dfs(parentToChild, nextNode, checkedSet, visitedSet):
                return False
        visitedSet.remove(node)
        return True

    def buildGraph(self, numCourses, prerequisites):
        childToParent = [set() for _ in range(numCourses)]
        parentToChild = [set() for _ in range(numCourses)]
        for relation in prerequisites:
            parent = relation[0]
            child = relation[1]
            childToParent[child].add(parent)
            parentToChild[parent].add(child)
        return childToParent, parentToChild
```
