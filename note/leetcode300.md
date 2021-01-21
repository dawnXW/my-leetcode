# leetcode300

[题目描述](https://leetcode-cn.com/problems/longest-increasing-subsequence/comments/)

<br>

可以看出是dp问题，那么，是否可以快速的估算出dp算法的时间复杂度？

<br>

可以分析出，长度为n的列表X，遍历的时候，包含2个状态，一个是把第n个是数算进去的时候，最长的长度，还有是不把n算尽去的时候，最长的长度，两个去较大值。

<br>

即包含的状态 dp_include[n] = max(dp_include[k1]+1, dp_include[k2]+1, dp_include[k3]+1, ...) 其中 k1,k2,k3 都满足 X[k*] < X[n]

<br>

和不包含的状态 dp_exclude[n] = max(dp_include[1], ... , dp_include[n-1])

<br>

综合一下，最大值就是 max(dp_include[1], ... dp_include[n]

<br>

所以只要计算包含状态，最后从所有的包含状态中取最大值即可。

<br>

dp如果 n 只和 n-1 的状态有关，列表数据时的时间复杂度一般是 O(n)，如果 n 和之前所有的状态都有关，时间复杂度一般是 O(n^2)。
