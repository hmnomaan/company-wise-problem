### 1025 · Custom Sort String
Algorithms
Medium
Accepted Rate
54%



### Description
S and T are strings composed of lowercase letters. In S, no letter occurs more than once.

S was sorted in some custom order previously. We want to permute the characters of T so that they match the order that S was sorted. More specifically, if x occurs before y in S, then x should occur before y in the returned string.

The characters in the string T that do not exist in S are placed at the end of the string in dictionary order.

## (i) 
S has length at most 26, and no character is repeated in S.
T has length at most 200.
S and T consist of lowercase letters only.


## Example
```python
Example :
Input: 
S = "cba"
T = "abcd"
Output: "cbad"
Explanation: 
"a", "b", "c" appear in S, so the order of "a", "b", "c" should be "c", "b", and "a".
Since "d" does not appear in S, it is placed at the end of T.

```
```python


```
### SOLVE this:

```python
class Solution:
    """
    @param s: The given string S
    @param t: The given string T
    @return: any permutation of T (as a string) that satisfies this property
    """
    def custom_sort_string(self, s: str, t: str) -> str:
        # Write your code here

```

### Tags
Sort

## Company
Company
Facebook
Amazon


### Related Problems
Related Problems

49
Sort Letters by Case
Medium

656
Multiply Strings
Medium





### best answer
```py
class Solution:
    """
    @param s: The given string S
    @param t: The given string T
    @return: any permutation of T (as a string) that satisfies this property
    """
    def custom_sort_string(self, s: str, t: str) -> str:
        # Write your code here
        countT=collections.defaultdict(int)
        for c in t:
            countT[c]+=1
        res=[]
        for c in s:
            if c in countT:
                res.append(c*countT[c])
                del countT[c]

        for k in sorted(countT.keys()):
            res.append(k*countT[k])
        return "".join(res)
```
```py
class Solution:
    """
    @param s: The given string S
    @param t: The given string T
    @return: any permutation of T (as a string) that satisfies this property
    """
    def custom_sort_string(self, s: str, t: str) -> str:
        # Write your code here
        countT=collections.defaultdict(int)
        for c in t:
            countT[c]+=1
        res=[]
        for c in s:
            if c in countT:
                res.append(c*countT[c])
                del countT[c]

        for k in sorted(countT.keys()):
            res.append(k*countT[k])
        return "".join(res)
```


### Official answer from lintcode

```py
class Solution:
    """
    @param S: The given string S
    @param T: The given string T
    @return: any permutation of T (as a string) that satisfies this property
    """
    def customSortString(self, S, T):
        # Write your code here
        res = ""
        cnt, t = [0] * 26, 0
        for i in range(0, len(T)):
        	cnt[ord(T[i]) - ord('a')] += 1
        for i in range(0, len(S)):
        	for j in range(0, cnt[ord(S[i]) - ord('a')]):
        		res += S[i]
        	cnt[ord(S[i]) - ord('a')] = 0
        for i in range(0, 26):
        	for j in range(0, cnt[i]):
        		res += chr(ord('a') + i)
        return res
```
--- >  > > Count the characters in t with counter Spell them in the order of s Put the remaining characters in t that are not in s at the end in lexicographic order It is best to put the string in a list first and join it at the end, so that the time complexity is the lowest

```py
class Solution:
    """
    @param s: The given string S
    @param t: The given string T
    @return: any permutation of T (as a string) that satisfies this property
    """
    def custom_sort_string(self, s: str, t: str) -> str:
        # Write your code here
        counter = collections.Counter(t)
        result = []

        for c in s:
            if c in counter:
                freq = counter[c]
                result += [c] * freq
                counter.pop(c)

        for c in sorted(counter.keys()):
            result += [c] * counter[c]

        return ''.join(result)
```