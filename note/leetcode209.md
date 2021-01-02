# leetcode209
[题目描述](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)
<br>
用一个deque，贪心算法即可。
```python
class Solution(object):
    def minSubArrayLen(self, s, nums):
        if sum(nums) < s:
            return 0
        length = sys.maxint
        currentsum = 0
        d = collections.deque()
        for num in nums:
            currentsum += num
            d.append(num)
            if currentsum >= s:
                while currentsum >= s:
                    x = d.popleft()
                    currentsum -= x
                length = min(length, len(d)+1)
        return length
```
