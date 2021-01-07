# leetcode322
[题目描述](https://leetcode-cn.com/problems/coin-change/)


<br>
用回溯法确定能否满足条件


```python
class Solution(object):

    def coinChange(self, coins, amount):
        self.dp_set = set()
        self.coins = coins
        coins.sort(reverse=True)
        return self.backtrack(amount)

    def backtrack(self, amount):
        if amount in self.dp_set:
            return False

        for coin in self.coins:
            if coin == amount:
                return True
            if coin > amount:
                break
            if self.backtrack(amount - coin):
                return True

        self.dp_set.add(amount)
        return False
```


<br>
但是题目的要求是求出最小硬币数量。需要一个横向（Array）的dp。


```python
class Solution(object):
    def coinChange(self, coins, amount):
        coins.sort()

        dp = [sys.maxint for i in range(amount + 1)]
        dp[0] = 0
        res = sys.maxint

        for i in range(1, amount + 1):
            for coin in coins:
                if i < coin:
                    break
                dp[i] = min(dp[i], dp[i - coin] + 1)
        print dp[90:100]
        return dp[amount] if dp[amount] != sys.maxint else -1
```


<br>
耗时最少的解法，是从后向前遍历，没有dp，思路是，这样可以及时停止遍历


```python
class Solution(object):
    def coinChange(self, coins, amount):
        def coinChanging(coins, amount, c_index, count, ans):
            if amount == 0:
                return min(ans, count)
            if c_index == len(coins):
                return ans
            k = amount // coins[c_index]
            while k >= 0 and k + count < ans:
                ans = coinChanging(coins, amount - k * coins[c_index], c_index + 1, count + k, ans)
                k -= 1
            return ans

        if amount == 0:
            return 0
        coins.sort(reverse=True)
        ans = coinChanging(coins, amount, 0, 0, float('inf'))
        return ans if ans != float('inf') else -1
```
