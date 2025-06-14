### 1481 · Unique Substring
Algorithms
Medium
Accepted Rate
72%


### Description
Given a string s, find all the unique substring with the length of k and sort the results in lexicographic order.




## Example
```python
Input: s = "caaab"，k = 2
Output:["aa","ab","ca"]
Explanation:
two adjacent lengths of strings are split and duplication removed

```
```python
Input: s = "aaaa"，k = 3
Output:["aaa"]
Explanation:
three adjacent lengths of strings are split and duplication removed

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param s: a string
    @param k: an integer
    @return: all unique substring
    """
    def unique_substring(self, s: str, k: int) -> List[str]:
        # Write your code here

```

### Tags
Hash Table
## Company
Amazon

### Related Problems






### best answer
```py
class Solution:
    """
    @param s: a string
    @param k: an integer
    @return: all unique substring
    """
    def uniqueSubstring(self, s, k):
        # Write your code here
        return sorted({s[idx-k:idx] for idx in range(k,len(s)+1)})
```
```py
class Solution:
    """
    @param s: a string
    @param k: an integer
    @return: all unique substring
    """
    def uniqueSubstring(self, s, k):
        res = set()
        for i in range(0, len(s)-k+1):
            res.add(s[i:i+k])
        res = [string for string in res]
        return sorted(res)
```
```py
class Solution:
    """
    @param stringIn: The original string.
    @param K: The length of substrings.
    @return: return the count of substring of length K and exactly K distinct characters.
    """
    def uniqueSubstring(self, s, k):
        if len(s) < k or k == 0:
            return []
        
        count = 0
        result = set([s[:k]])
        for i in range(1, len(s) - k + 1):

            result.add(s[i:i + k])
        return sorted(result)
```


### Official answer from lintcode
考点：

set
题解：
题目指定截取字串长度，故只需遍历一次每处截取k长度字串存入即可(注意判断leng-i>=k)，答案要求去重和排序，使用set去重，转化list排序即可。
```py
class Solution:
    """
    @param s: a string
    @param k: an integer
    @return: all unique substring
    """
    def uniqueSubstring(self, s, k):
        # Write your code here
        ans=set()
        leng=len(s)
        for i in range(leng) :
            if leng-i>=k:
                ans.add(s[i:i+k])
            else :
                break
        res=list(ans)
        res.sort()
        return res
```
//
2
O(nlogn) time because of sorting, O(n) space for sure
```py
class Solution:
    """
    @param s: a string
    @param k: an integer
    @return: all unique substring
    """
    def uniqueSubstring(self, s, k):
        return sorted(list(set(s[i:i+k] for i in range(len(s) - k + 1))))
```