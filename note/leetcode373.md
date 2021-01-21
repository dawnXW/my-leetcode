# leetcode373

[题目描述](https://leetcode-cn.com/problems/find-k-pairs-with-smallest-sums/)

<br>

因为是固定从num1和num2各取一个数字，所以可以对每个num1记录一个当前对应num2的指针。

```python
class Solution(object):
    def kSmallestPairs(self, nums1, nums2, k):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type k: int
        :rtype: List[List[int]]
        """
        res = []
        N1 = len(nums1)
        N2 = len(nums2)
        if not N1 or not N2:
            return res
        k = min(N1 * N2, k) # k的最大值是N1*N2
        pointerList = [0] * N1
        tmpMinList = [nums2[0]+nums1[i] for i in xrange(N1)]
        while len(res) < k:
            cur_min = tmpMinList[0]
            cur_min_pos = 0
            for i in range(1, N1):
                if cur_min > tmpMinList[i]:
                    cur_min_pos = i
                    cur_min = tmpMinList[i]
            #print cur_min_pos, pointerList[cur_min_pos]
            res.append((nums1[cur_min_pos], nums2[pointerList[cur_min_pos]]))
            num2_pos = pointerList[cur_min_pos]
            num2_pos += 1
            pointerList[cur_min_pos] = num2_pos
            if num2_pos == N2:
                tmpMinList[cur_min_pos] = sys.maxint
            else:
                tmpMinList[cur_min_pos] = nums1[cur_min_pos] + nums2[num2_pos]
        return res
```

<br>

用heap的性能会更好，每次增加2各，它的左边，和它的右边

<br>

**注** ： heappush可以对一个数组生效，用数组中的第一个值排序
