# leetcode343
[题目描述](https://leetcode-cn.com/problems/integer-break/)

<br>
根据Hint2 You may check the breaking results of n ranging from 7 to 10 to discover the regularities.

| n   | result                 |
| --- | ---------------------- |
| 7   | 2 * 2 * 3 = 12         |
|     | 3 * 4 = 12             |
| 8   | 2 * 2 * 2 * 2 = 16     |
|     | 3 * 3 * 2 = 18         |
|     | 4 * 4 = 16             |
| 9   | 2 * 2 * 2 * 3 = 24     |
|     | 3 * 3 * 3 = 27         |
|     | 4 * 5 = 20             |
| 10  | 5 * 5 = 25             |
|     | 3 * 3 * 4 = 36         |
|     | 2 * 2 * 3 * 3 =36      |
|     | 2 * 2 * 2 * 2 * 2 = 32 |

<br>

~~看着是一个动态规划的问题~~

<br>


是一个数学问题

<br>

因为分成n个数，每个数约接近，这n个数的乘积就越大，问题变成，x * y = n 求 max( x^y )，目前看x与y越接近，值越大，求证？

<br>

```
n = a ^ 2, a 个 a 连乘
a ^ a (1)
n = (a+1) * (a-1) + 1，(a-2)个（a+1）连乘，再乘一个a
a * (a+1)^(a-2) (2)

(1)(2)相除
( a ^ (a-1) ) / ( (a+1)^(a-2) ) = a * (a/(a+1))^(a-2)
反回来
(1/a) * (1+(1/a))^(a-2) (杨辉三角形)
(1/a) * (1+(a-2)(1/a)
```

错误，事实应该对 x ^ (n/x) 求导数，当导数为0是，x=e，相比2，更接近3，所以尽量多的分成3

```
class Solution(object):
    def integerBreak(self, n):
        if n == 2:
            return 1
        if n == 3:
            return 2
        if n == 4:
            return 4

        x = n // 3
        y = n % 3
        if y == 0:
            return pow(3, x)
        elif y == 1:
            return pow(3, x-1) * 4
        elif y == 2:
            return pow(3, x) * 2
```
