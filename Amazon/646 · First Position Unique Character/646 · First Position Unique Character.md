### 646 · First Position Unique Character
Algorithms
Easy
Accepted Rate
41%


### Description

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.



## Example
```python
Input : s = "lintcode"
Output : 0

```
```python
Input : s = "lovelintcode"
Output : 2

```
### SOLVE this:

```python
class Solution:
    """
    @param s: a string
    @return: it's index
    """
    def first_uniq_char(self, s: str) -> int:
        # write your code here

```

### Tags
Hash Table
String


## Company
Company
Bloomberg
Amazon
Microsoft

### Related Problems
Related Problems

960
First Unique Number in Data Stream II
Medium





### best answer
```py
class Solution:
    """
    @param s: a string
    @return: it's index
    """
    def first_uniq_char(self, s: str) -> int:
        # write your code here
        from collections import Counter
        counter = Counter(s)

        for i, ch in enumerate(s):
            if counter[ch] == 1:
                return i
        return -1
```


### Official answer from lintcode
First scan all the characters, save the characters that have appeared, then scan again, and the first character that appears once is the answer.
```py
class Solution:
    # @param {string} s a string
    # @return {int} it's index
    def firstUniqChar(self, s):
        # Write your code here
        alp = {}
        for c in s:
            if c not in alp:
                alp[c] = 1
            else:
                alp[c] += 1

        index = 0
        for c in s:
            if alp[c] == 1:
                return index
            index += 1
        return -1
```