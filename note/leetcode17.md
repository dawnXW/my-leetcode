# leetcode17
[题目内容](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)
<br>
**主观感受** 需要使用BFS或者DFS的方法，又分为递归和不递归，应该有4种解法
<br>
**正向BFS**<br>
```kbd_map``` 如果是```str : str```的形式，性能会慢很多
<br>

```python
class Solution(object):
    kbd_map = {
        "2" : ["a", "b", "c"],
        "3" : ["d", "e", "f"],
        "4" : ["g", "h", "i"],
        "5" : ["j", "k", "l"],
        "6" : ["m", "n", "o"],
        "7" : ["p", "q", "r", "s"],
        "8" : ["t", "u", "v"],
        "9" : ["w", "x", "y", "z"]
    }
    def letterCombinations(self, digits):
        res = []
        for num in digits:
            kbd = self.kbd_map[num]
            if len(res) == 0:
                for c in kbd:
                    res.append(c)
            else:
                tmp_res = []
                for prev_str in res:
                    for c in kbd:
                        cur_str = prev_str + c
                        tmp_res.append(cur_str)
                res = tmp_res
        return res
```
<br>

**反向BFS（递归）**<br>
```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        mDict = {'2':'abc','3':'def','4':'ghi','5':'jkl','6':'mno','7':'pqrs','8':'tuv','9':'wxyz'}
        if len(digits) == 0:
            return []
        if len(digits) == 1:
            return  [a for a in mDict[digits]]
        result  = []
        for a in mDict[digits[0]]:
            for x in self.letterCombinations(digits[1:]):
                result.append(a+x)
        return result
```
<br>
<br>
<br>

**DFS**<br>

```python
class Solution:
    def letterCombinations(self, digits: str) -> list:
        KEY = {'2': ['a', 'b', 'c'],
               '3': ['d', 'e', 'f'],
               '4': ['g', 'h', 'i'],
               '5': ['j', 'k', 'l'],
               '6': ['m', 'n', 'o'],
               '7': ['p', 'q', 'r', 's'],
               '8': ['t', 'u', 'v'],
               '9': ['w', 'x', 'y', 'z']}
        if digits == '':
            return []
        ans = ['']
        for num in digits:
            ans = [pre+suf for pre in ans for suf in KEY[num]]
        return ans
```
