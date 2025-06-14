### 647 · Find All Anagrams in a String
Algorithms
Medium
Accepted Rate
37%


### Description

Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.
If s is an anagram of p, then s is a permutation of p.
Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 40,000.
The order of output does not matter.



## Example
```python
Input : s =  "cbaebabacd", p = "abc"
Output : [0, 6]
Explanation : 
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".

```
```python


```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param s: a string
    @param p: a string
    @return: a list of index
    """
    def find_anagrams(self, s: str, p: str) -> List[int]:
        # write your code here

```

### Tags
Same Direction Two Pointers
Two Pointers


## Company
Amazon

### Related Problems

Related Problems

158
Valid Anagram
Easy

171
Anagrams
Medium

772
Group Anagrams
Medium

1169
Permutation in String
Medium




### best answer
```py
from typing import (
    List,
)

class Solution:
    """
    @param s: a string
    @param p: a string
    @return: a list of index
    """
    def find_anagrams(self, s: str, p: str) -> List[int]:
        result = []
        char_counts = {}
        for char in p:
            char_counts[char] = char_counts.get(char, 0) + 1
        
        left = 0
        match_count = 0 
        
        for right in range(len(s)):
            current_char = s[right]
            
            if current_char in char_counts:
                char_counts[current_char] -= 1
                if char_counts[current_char] >= 0:
                    match_count += 1
            
            if right - left + 1 == len(p):
                if match_count == len(p):
                    result.append(left)
                
                char_to_remove = s[left]
                if char_to_remove in char_counts:
                    if char_counts[char_to_remove] >= 0:
                        match_count -= 1
                    char_counts[char_to_remove] += 1
                
                left += 1
                
        return result
```
```py
from typing import (
    List,
)
from collections import Counter
class Solution:
    """
    @param s: a string
    @param p: a string
    @return: a list of index
    """
    def find_anagrams(self, s: str, p: str) -> List[int]:
        # write your code here
        if len(p) > len(s):
          return []
        
        counter_p = Counter()
        for ch in p:
          counter_p[ch] += 1

        def check(counter, counter_p):
          for k, v in counter_p.items():
            if k not in counter or v != counter[k]:
              return False
          return True
        counter = Counter()
        ans = [] 
        # a, b, c 3
        for i in range(len(s)):
          counter[s[i]] += 1
          if i < len(p) - 1: # 2, i == 2
            continue
          # i >= 2
          if check(counter, counter_p):
            ans.append(i - len(p) + 1)
          counter[s[i - len(p) + 1]] -= 1
        return ans

          
          



```


### Official answer from lintcode
Since it has nothing to do with the order, you can open an array to record the number of each character, and once the number of characters in the p string is met, record the answer.
```py
class Solution:
    # @param {string} s a string
    # @param {string} p a non-empty string
    # @return {int[]} a list of index
    def findAnagrams(self, s, p):
        # Write your code here
        ans = []
        sum = [0 for x in range(0,30)]
        plength = len(p)
        slength = len(s)
        for i in range(plength):
            sum[ord(p[i]) - ord('a')] += 1
        start = 0
        end = 0
        matched = 0
        while end < slength:
            if sum[ord(s[end]) - ord('a')] >= 1:
                matched += 1
            sum[ord(s[end]) - ord('a')] -= 1
            end += 1
            if matched == plength:
                ans.append(start)
            if end - start == plength:
                if sum[ord(s[start]) - ord('a')] >= 0:
                    matched -= 1
                sum[ord(s[start]) - ord('a')] += 1
                start += 1
        return ans
```