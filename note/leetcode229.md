# leetcode229
[题目描述](https://leetcode-cn.com/problems/majority-element-ii/)

## Naive Idea
排序后计数，实际复杂度```O(nlgn)```
```python
class Solution(object):
    def majorityElement(self, nums):
        N = len(nums)
        N_div_3 = N // 3
        if N < 1:
            return False
        nums.sort()
        cnt = 1
        pre = nums[0]
        res = []
        for i in xrange(1, N):
            if nums[i] == pre:
                cnt += 1
            else:
                if cnt > N_div_3:
                    res.append(pre)
                pre = nums[i]
                cnt = 1
        if cnt > N_div_3:
            res.append(pre)
        return res
```

## Dict Count
```python
class Solution(object):
    def majorityElement(self, nums):
        N = len(nums)
        N_div_3 = N // 3
        countDict = {}
        for num in nums:
            countDict[num] = countDict.get(num, 0)+1
        res = []
        for num in countDict.keys():
            if countDict[num] > N_div_3:
                res.append(num)
        return res
```

## 摩尔投票法
**提问：**给定一个int型数组，找出该数组中出现次数大于数组长度一半的int值。
<br>**摩尔投票法**的基本思想很简单，在每一轮投票过程中，从数组中找出一对不同的元素，将其从数组中删除。这样不断的删除直到无法再进行投票，如果数组为空，则没有任何元素出现的次数超过该数组长度的一半。如果只存在一种元素，那么这个元素则可能为目标元素。
