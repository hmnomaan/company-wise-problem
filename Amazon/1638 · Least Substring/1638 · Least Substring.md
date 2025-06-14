### 1638 · Least Substring

Algorithms
Easy
Accepted Rate
54%

### Description

Given a string containing n lowercase letters, the string needs to be divided into several continuous substrings, the letter in the substring should be same, and the number of letters in the substring does not exceed k, and output the minimal substring number meeting the requirement.

## (i)

n≤1e5

## Example

```python
Input: s = "aabbbc", k = 2
Output: 4
Explanation:
we can get "aa", "bb", "b", "c" four substring.

```

```python
input: s = "aabbbc", k = 3
Output: 3
we can get "aa", "bbb", "c" three substring.

```

### SOLVE this:

```python
class Solution:
    """
    @param s: the string s
    @param k: the maximum length of substring
    @return: return the least number of substring
    """
    def get_ans(self, s: str, k: int) -> int:
        # Write your code here

```

### Tags

String

## Company

Amazon

### Related Problems

### best answer

```py
class Solution:
    """
    @param s: the string s
    @param k: the maximum length of substring
    @return: return the least number of substring
    """
    def getAns(self, s, k):
        cnt = 1
        ans = 1

        for i in range(1, len(s)):
            if s[i] == s[i-1] and cnt < k:
                cnt += 1
            else:
                ans += 1
                cnt = 1
        return ans
```

```py
class Solution:
    """
    @param s: the string s
    @param k: the maximum length of substring
    @return: return the least number of substring
    """
    def get_ans(self, s: str, k: int) -> int:
        # 最终结果：最少划分的子串数。
        res = 0
        # 保留上一个字符
        last_c = '\0'
        # 与当前字符相同的字符重复的次数。
        cur = 0
        # 对字符串 s 进行遍历，每次拿到当前的字符 c。
        for c in s:
            # 如果当前的字符和上个字符相同。
            if c == last_c:
                # 记录本子串的长度加 1。
                cur += 1
                # 如果本子串的长度已经大于 k，则需要开启一个新的子串。
                if cur > k:
                    # 将最终的划分计数加 1。
                    res += 1
                    # 当前子串的长度设为 1。
                    cur = 1
                continue;
            # 如果当前字符和上个字符不同。 需要更新相关状态，让当前子串长度设为 1。
            cur = 1
            # 更新上个字符的变量。
            last_c = c
            # 将最终的划分计数加 1。
            res += 1
        # 返回最终的划分数。
        return res
# 解题方法：

# 定义一个字符变量保存上个字符是什么，初始设为一个非英文字符。
# 定义两个整型变量，一个记录最终的划分数，另一个记录当前划分的长度。
# 遍历字符串
# 如果当前字符不等于上个字符，则划分数加 1，当前划分的长度设为 1。
# 如果当前字符等于上个字符且当前划分长度小于 k，则当前划分长度加 1。
# 如果当前字符等于上个字符且当前划分长度等于 k，则划分数加 1，当前划分的长度设为 1。
# 返回最终划分数。
```

```py
class Solution:
    """
    @param s: the string s
    @param k: the maximum length of substring
    @return: return the least number of substring
    """
    def getAns(self, s, k):
        # Write your code here
        
        print(s)
        rt, pre_c = 0, ''
        for c in s:
            if c == pre_c and cnt < k:
                cnt += 1
            else:
                rt += 1
                cnt = 1
            pre_c = c
        
        return rt
```

```py
class Solution:
    """
    @param s: the string s
    @param k: the maximum length of substring
    @return: return the least number of substring
    """
    def get_ans(self, s: str, k: int) -> int:
        # Write your code here

        if not s:
            return 0

        if k == 1:
            return len(s)

        cnt = 0
        c = s[0]
        ans = 0
        for i in range(len(s)):
            #print(i, cnt, s[i], ans)
            if c == s[i]:
                cnt += 1

                if cnt == k:
                    ans += 1
                    cnt = 0
            else:
                if cnt != 0:
                    ans += 1

                c = s[i]
                cnt = 1

            #print(i, cnt, s[i], ans)

        if cnt > 0:
            ans += 1

        return ans
```

### Official answer from lintcode

//1
解题思路
本题知识点：计数。

计数
遍历输入字符串，有两种情况进行增加划分：

当前字符与上个字符不相同。
相同字符的划分长度大于 k。
遍历完毕即可计算得到所要求的划分数。

如样例 1， 字符串为 aabbbc，且 k = 2 。
![alt text](image.png)
按照计数的方法，可以得到有 4 个划分。

解题方法：

定义一个字符变量保存上个字符是什么，初始设为一个非英文字符。
定义两个整型变量，一个记录最终的划分数，另一个记录当前划分的长度。
遍历字符串
如果当前字符不等于上个字符，则划分数加 1，当前划分的长度设为 1。
如果当前字符等于上个字符且当前划分长度小于 k，则当前划分长度加 1。
如果当前字符等于上个字符且当前划分长度等于 k，则划分数加 1，当前划分的长度设为 1。
返回最终划分数。
复杂度分析
空间复杂度：
O
(
1
)
O(1)，额外需要常数个变量。
时间复杂度：
O
(
n
)
O(n)，遍历一遍原字符串即可，
n
n 为字符串长度。

题解代码

```py
class Solution:
    """
    @param s: the string s
    @param k: the maximum length of substring
    @return: return the least number of substring
    """
    def get_ans(self, s: str, k: int) -> int:
        # 最终结果：最少划分的子串数。
        res = 0
        # 保留上一个字符
        last_c = '\0'
        # 与当前字符相同的字符重复的次数。
        cur = 0
        # 对字符串 s 进行遍历，每次拿到当前的字符 c。
        for c in s:
            # 如果当前的字符和上个字符相同。
            if c == last_c:
                # 记录本子串的长度加 1。
                cur += 1
                # 如果本子串的长度已经大于 k，则需要开启一个新的子串。
                if cur > k:
                    # 将最终的划分计数加 1。
                    res += 1
                    # 当前子串的长度设为 1。
                    cur = 1
                continue;
            # 如果当前字符和上个字符不同。 需要更新相关状态，让当前子串长度设为 1。
            cur = 1
            # 更新上个字符的变量。
            last_c = c
            # 将最终的划分计数加 1。
            res += 1
        # 返回最终的划分数。
        return res
```

//2
这道题字符串分段有两种情况
当前相同字符长度为 k，或者字符不匹配
用 for 循环更新 flag 字符和新段子的字符长度

```py
class Solution:
    """
    @param s: the string s
    @param k: the maximum length of substring
    @return: return the least number of substring
    """
    def getAns(self, s, k):
        # Write your code here
        n = len(s)
        ans = 1
        cnt = 1;
        for i in range (1,n):
            if (s[i] == s[i-1] and cnt < k) :
                cnt += 1
            else :
                ans += 1
                cnt = 1
        return ans;
```
