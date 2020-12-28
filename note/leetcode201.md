# leetcode201
[题目内容](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/)
<br>
最初的感觉是一道纯数学题，代码上只需要掌握基本的位运算
<br>
我的思路是这样，```n-m```的位数```x```，```(m >> x) << x```就是返回的值

| 十进制 | 二进制 | 十进制 | 二进制 |
| ------ | ------ | ------ | ------ |
| 0      | 0000   | 8      | 1000   |
| 1      | 0001   | 9      | 1001   |
| 2      | 0010   | 10     | 1010   |
| 3      | 0011   | 11     | 1011   |
| 4      | 0100   | 12     | 1100   |
| 5      | 0101   | 13     | 1101   |
| 6      | 0110   | 14     | 1110   |
| 7      | 0111   | 15     | 1111   |

这是有问题的，如上表中，```m=15,n=14```满足，但是如果```m=15,n=9```就不满足。
<br>
正确的解法是找到```m```和```n```完全**相等**的部分。
```python
class Solution(object):
    def rangeBitwiseAnd(self, m, n):
        cnt = 0
        while m > 0 and m != n:
            m >>= 1
            n >>= 1
            cnt += 1
        return m << cnt
```