# leetcode220
[题目链接](https://leetcode-cn.com/problems/contains-duplicate-iii/)
## brutal force
这道题的算法部分
```python
class Solution(object):
    def containsNearbyAlmostDuplicate(self, nums, k, t):
        N = len(nums)
        if N < 2 or k < 1:
            return False
        aRange = N-1
        for i in xrange(aRange):
            a = nums[i]
            bRange = min(N-1, i+k)+1
            for j in xrange(i+1, bRange):
                if abs(a-nums[j]) <= t:
                    return True
        return False
```
算法只需重复执行，把```nums[i], 0 <= i < N-1```作为第一个被减数，往后找```nums[j], i < j < min(N, i+k)```，作为第二个被减数，重复比较即可，时间复杂度是```O(kN)```。

## 类似桶排序
这道题的数据结构部分
```python
class Solution(object):
    def containsNearbyAlmostDuplicate(self, nums, k, t):
        N = len(nums)
        if N < 2 or k < 1 or t < 0:
            return False
        buckets = {}
        t += 1
        for i in xrange(N):
            if i > k:
                buckets.pop(nums[i-k-1] // t)
            a = nums[i]
            key = a // t
            if buckets.has_key(key):
                return True
            if buckets.has_key(key+1) and buckets[key+1]-a < t:
                return True
            if buckets.has_key(key-1) and a-buckets[key-1] < t:
                return True  
            buckets[key] = a
        return False
```
