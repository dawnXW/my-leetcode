# leetcode215
[题目描述](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)
<br>
## 最小堆
```python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        heap = []
        for num in nums:
            heapq.heappush(heap, num)
            if len(heap) > k:
                heapq.heappop(heap)
        return heapq.heappop(heap)
```
发现没哟```nums.sort()```块。
