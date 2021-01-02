# leetcode309
[题目描述](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
<br>
因为有冷冻期，所以是动态规划。
<br>
没有冷冻期，用贪心算法。
<br>
有三种状态，未持有，持有，冷冻期
<br>
<br>
**递推关系**

| 状态   | n收益 | n持有日期 | n+1收益                  | n+1持有日期      |
| ------ | ----- | --------- | ------------------------ | ---------------- |
| 未持有 | A(n)  | None      | max(A(n),C(n))           | None             |
| 持有   | B(n)  | Date(n)   | max(A(n),B(n))           | n+1 或者 Date(n) |
| 冷冻期 | C(n)  | None      | B(n)+(x(n+1)-x(Date(n))) | None             |

<br>

## 动态规划
```python
class Solution(object):
    def maxProfit(self, prices):
        if not prices:
            return 0
        A = 0
        date = 0
        B = -prices[date]
        C = 0
        for i in xrange(1, len(prices)):
            new_A = max(A, C)
            new_C = prices[i] + B
            if A - prices[i] > B:
                new_B = A - prices[i]
                date = i
            else:
                new_B = B
            A = new_A
            B = new_B
            C = new_C
        return max(A, B, C)
```
动态规划 + 贪心算法
<br>
我觉得动态规划对于分冶算法/图形算法来说是景上添花，但是对于贪心算法来说，<font color=red>可以解决简单贪心算法不能解决的问题，是贪心算法的升级版</font>。
