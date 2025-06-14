### 624 · Remove Substrings
Algorithms
Medium
Accepted Rate
41%


### Description

Given a string s and a list of strings dict, do the following repeatedly for s until none of the strings in dict are substrings of s.

If a string in dict is a substring of s, remove that substring from s
If more than one string in dict is a substring of s, remove any one of the strings s
Design a scheme that minimizes the length of the removed s and returns this minimum length.

## (i) A substring is a part of string that deleted a prefix and a postfix.



## Example
Example
Example 1:

```python
Input:
"ccdaabcdbb"
["ab","cd"]
Output:
2
Explanation: The following operations are performed in order:
s = "ccda[ab]cdbb", deleting "ab" starting with subscript 4 to get s = "ccdacdbb"
s = "c[cd]acdbb", delete "cd" starting with subscript 1 to get s = "cacdbb"
s = "ca[cd]bb", delete "cd" starting with subscript 2 to get s = "cabb"
s = "c[ab]b", delete "ab" starting with subscript 1 to get s = "cb"

The substring of s no longer exists in the dict, and the final length of s is 2



```

Example 2: 
```python
Input:
"abcabd"
["ab","abcd"]
Output:
0
Explanation: 
abcabd -> abcd -> "" (length = 0)
```
### SOLVE this:

```py
from typing import (
    Set,
)

class Solution:
    """
    @param s: a string
    @param dict: a set of n substrings
    @return: the minimum length
    """
    def min_length(self, s: str, dict: Set[str]) -> int:
        # write your code here
```




### Tags
Breadth First Search/BFS

## Company
Amazon

### Related Problems






### best answer
```py
from collections import deque
class Solution:
    """
    @param s: a string
    @param dict: a set of n substrings
    @return: the minimum length
    """
    def minLength(self, s, dict):
        substrings = dict
        if not s:
            return 0
        if not substrings:
            return len(s)
        
        min_len = len(s)
        queue = deque([s])
        visited = set([s])
        
        while queue:
            cur_str = queue.popleft()
            #print(cur_str)
            for sub in substrings:
                found = cur_str.find(sub)
                while found != -1:
                    new_str = cur_str[: found] + cur_str[found + len(sub): ]
                    if new_str not in visited:
                        if len(new_str) <= min_len:
                            queue.append(new_str)
                            visited.add(new_str)
                            min_len = len(new_str)
                    found = cur_str.find(sub, found + 1)
        #print(min_len)
        return min_len
```


### Official answer from lintcode

```py
class Solution:
    # @param {string} s a string
    # @param {set} dict a set of n substrings
    # @return {int} the minimum length
    def minLength(self, s, dict):
        # Write your code here
        import Queue
        que = Queue.Queue()
        que.put(s)
        hash = set([s])
    
        min = len(s)

        while not que.empty():
            s = que.get()
            for sub in dict:
                found = s.find(sub)
                while found != -1:
                    new_s = s[:found] + s[found + len(sub):]
                    if new_s not in hash:
                        if len(new_s) < min:
                            min = len(new_s)
                        que.put(new_s)
                        hash.add(new_s)

                    found = s.find(sub, found + 1)
        return min
```