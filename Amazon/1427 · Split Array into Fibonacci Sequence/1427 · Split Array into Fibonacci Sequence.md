### 1427 · Split Array into Fibonacci Sequence
Algorithms
Medium
Accepted Rate
51%


### Description
Given a string S of digits, such as S = "123456579", we can split it into a Fibonacci-like sequence [123, 456, 579].

Formally, a Fibonacci-like sequence is a list F of non-negative integers such that:

0 <= F[i] <= 2^31 - 1, (that is, each integer fits a 32-bit signed integer type);
F.length >= 3;
F[i] + F[i+1] = F[i+2] for all 0 <= i < F.length - 2.
Also, note that when splitting a string into small blocks, the number of each block must not start with zero, unless the block is the number 0 itself.

Return any Fibonacci-like sequence split from S, or return [] if it cannot be done.

## (i)

1 <= S.length <= 200
S contains only digits.


## Example
```python
Example 1:

Input: "123456579"
Output: [123,456,579]

```
```python
Example 2:

Input: "11235813"
Output: [1,1,2,3,5,8,13]

```
```python
Example 3:

Input: "112358130"
Output: []
Explanation: The task is impossible.

```
```python
Example 4:

Input: "0123"
Output: []
Explanation: Leading zeroes are not allowed, so "01", "2", "3" is not valid.

```
```python
Example 5:

Input: "1101111"
Output: [110, 1, 111]
Explanation: The output [11, 0, 11, 11] would also be accepted.

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param s: a string S of digits
    @return: Return any Fibonacci-like sequence split from S
    """
    def split_into_fibonacci(self, s: str) -> List[int]:
        # write your code here

```

### Tags
Depth First Search/DFS
Greedy
String

## Company
Amazon

### Related Problems






### best answer
1
```py
from typing import (
    List,
)

number = 0
txt = "\n"
class Solution:
    def split_into_fibonacci(self, s: str) -> List[int]:
        ans = list()

        def backtrack(index: int):
            if index == len(s):
                return len(ans) >= 3

            curr = 0
            for i in range(index, len(s)):
                if i > index and s[index] == "0":
                    break
                curr = curr * 10 + ord(s[i]) - ord("0")
                if curr > 2**31 - 1:
                    break

                if len(ans) < 2 or curr == ans[-2] + ans[-1]:
                    ans.append(curr)
                    if backtrack(i + 1):
                        return True
                    ans.pop()
                elif len(ans) > 2 and curr > ans[-2] + ans[-1]:
                    break

            return False

        backtrack(0)
        return ans
```
2
```py
from typing import (
    List,
)

class Solution:
    """
    @param s: a string S of digits
    @return: Return any Fibonacci-like sequence split from S
    """
    def split_into_fibonacci(self, s: str) -> List[int]:
        res = []
        max_split_size = min(10, len(s) // 2 + 1)  # Limit the length to prevent integer overflow
        for end in range(1, max_split_size):
            if s[0] == '0' and end > 1:
                break  # Leading zeros are not allowed
            num1 = int(s[:end])
            if num1 > 2**31 - 1:
                break  # Exceeds 32-bit integer limit
            for j in range(end + 1, len(s)):
                if s[end] == '0' and j - end > 1:
                    break
                num2 = int(s[end:j])
                if num2 > 2**31 - 1:
                    break
                path = [num1, num2]
                if self.dfs(s, j, path):
                    return path
        return []

    def dfs(self, s, idx, path):
        if idx == len(s):
            if len(path) >= 3:
                return True
            else:
                return False
        nxt = path[-1] + path[-2]
        if nxt > 2**31 - 1:
            return False  # Exceeds 32-bit integer limit
        nxt_str = str(nxt)
        if s.startswith(nxt_str, idx):
            path.append(nxt)
            if self.dfs(s, idx + len(nxt_str), path):
                return True
            path.pop()  # Backtrack after recursive call
        else:
            return False
        return False
     

```
3
```py
from typing import (
    List,
)

class Solution:
    def split_into_fibonacci(self, s: str) -> List[int]:
        ans = list()

        def backtrack(index: int):
            if index == len(s):
                return len(ans) >= 3

            curr = 0
            for i in range(index, len(s)):
                if i > index and s[index] == "0":
                    break
                curr = curr * 10 + ord(s[i]) - ord("0")
                if curr > 2**31 - 1:
                    break

                if len(ans) < 2 or curr == ans[-2] + ans[-1]:
                    ans.append(curr)
                    if backtrack(i + 1):
                        return True
                    ans.pop()
                elif len(ans) > 2 and curr > ans[-2] + ans[-1]:
                    break

            return False

        backtrack(0)
        return ans
# 回溯 + 剪枝
# 解题思路与方法
# 将给定的字符串拆分成斐波那契式序列，可以通过回溯的方法实现。

# 使用列表存储拆分出的数，回溯过程中维护该列表的元素，列表初始为空。遍历字符串的所有可能的前缀，作为当前被拆分出的数，然后对剩余部分继续拆分，直到整个字符串拆分完毕。

# 根据斐波那契式序列的要求，从第 
# 3
# 3 个数开始，每个数都等于前 
# 2
# 2 个数的和，因此从第 
# 3
# 3 个数开始，需要判断拆分出的数是否等于前 
# 2
# 2 个数的和，只有满足要求时才进行拆分，否则不进行拆分。

# 回溯过程中，还有三处可以进行剪枝操作。
```


### Official answer from lintcode
回溯 + 剪枝
解题思路与方法
将给定的字符串拆分成斐波那契式序列，可以通过回溯的方法实现。

使用列表存储拆分出的数，回溯过程中维护该列表的元素，列表初始为空。遍历字符串的所有可能的前缀，作为当前被拆分出的数，然后对剩余部分继续拆分，直到整个字符串拆分完毕。

根据斐波那契式序列的要求，从第 
3
3 个数开始，每个数都等于前 
2
2 个数的和，因此从第 
3
3 个数开始，需要判断拆分出的数是否等于前 
2
2 个数的和，只有满足要求时才进行拆分，否则不进行拆分。

回溯过程中，还有三处可以进行剪枝操作。

拆分出的数如果不是 
0
0，则不能以 
0
0 开头，因此如果字符串剩下的部分以 
0
0 开头，就不需要考虑拆分出长度大于 
1
1 的数，因为长度大于 
1
1 的数以 
0
0 开头是不符合要求的，不可能继续拆分得到斐波那契式序列；

拆分出的数必须符合 
32
32 位有符号整数类型，即每个数必须在 
[
0
,
2
31
−
1
]
[0,2 
31
 −1] 的范围内，如果拆分出的数大于 
2
31
−
1
2 
31
 −1，则不符合要求，长度更大的数的数值也一定更大，一定也大于 
2
31
−
1
2 
31
 −1，因此不可能继续拆分得到斐波那契式序列；

如果列表中至少有 
2
2 个数，并且拆分出的数已经大于最后 
2
2 个数的和，就不需要继续尝试拆分了。

当整个字符串拆分完毕时，如果列表中至少有 
3
3 个数，则得到一个符合要求的斐波那契式序列，返回列表。如果没有找到符合要求的斐波那契式序列，则返回空列表。

实现方面，回溯需要带返回值，表示是否存在符合要求的斐波那契式序列。

参考代码
```py
from typing import (
    List,
)

class Solution:
    def split_into_fibonacci(self, s: str) -> List[int]:
        ans = list()

        def backtrack(index: int):
            if index == len(s):
                return len(ans) >= 3

            curr = 0
            for i in range(index, len(s)):
                if i > index and s[index] == "0":
                    break
                curr = curr * 10 + ord(s[i]) - ord("0")
                if curr > 2**31 - 1:
                    break

                if len(ans) < 2 or curr == ans[-2] + ans[-1]:
                    ans.append(curr)
                    if backtrack(i + 1):
                        return True
                    ans.pop()
                elif len(ans) > 2 and curr > ans[-2] + ans[-1]:
                    break

            return False

        backtrack(0)
        return ans

```

```py
解题思路
很适合练习dfs，不是标准的排列和组合求解。属于字符串拆分问题。从index为0开始拆分，因为只需要求出满足条件的其中1个解，所以可以设置返回值。进行不满足条件的剪枝即可。无需使用全局变量。

题解代码
------
from typing import (
    List,
)

class Solution:
    """
    @param s: a string S of digits
    @return: Return any Fibonacci-like sequence split from S
    """
    def split_into_fibonacci(self, s: str) -> List[int]:
        ans = []
        self.dfs(s, 0, ans, len(s))
        return ans

    def dfs(self, s, index, ans, n):
        if index == n:
            return len(ans) >= 3

        curr = 0
        for i in range(index, n):
            if i > index and s[index] == '0':
                break
            curr = curr * 10 + int(s[i])
            if curr > 2 ** 31 - 1:
                break
            if len(ans) < 2 or curr == ans[-1] + ans[-2]:
                ans.append(curr)
                if self.dfs(s, i + 1, ans, n):
                    return True
                ans.pop()
            elif len(ans) > 2 and curr > ans[-1] + ans[-2]:
                break
        return False
```