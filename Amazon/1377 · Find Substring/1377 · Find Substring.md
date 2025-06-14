### 1377 · Find Substring
Algorithms
Medium
Accepted Rate
39%


### Description

Given the length k, find all substrings of length k in the string str.The characters of a substring can not be repeated and output the number of substrings that satisfy such conditions (the same substring is counted only 1 times).

## (i)

|str| <= 100000.
k <= 100000.
All characters are lowercase.

## Example
```python
Input:  str = "abc", k = 2
Output: 2
Explanation:
Characters are not repeated, and substrings of length k have "ab", "bc".

```
```python
Input: str = "abacb", k = 1
Output: 3
Explanation:
Characters are not repeated, and substrings of length k have "a", "b".”c”.

```
### SOLVE this:

```python
class Solution:
    """
    @param str: The string
    @param k: The length of the substring
    @return: The answer
    """
    def find_substring(self, str: str, k: int) -> int:
        # Write your code here

```

### Tags
Hash Table
String
Two Pointers

## Company
Amazon

### Related Problems






### best answer
```py
class Solution:
	"""
	@param str: The string
	@param k: The length of the substring
	@return: The answer
	"""
	def findSubstring(self, str, k):
		# Write your code here
		if k > 26:
			return 0
			
		subStrs = dict()
		subStr = ""
		# cnt = 0
		for char in str:
			if len(subStr) == k:
				# if subStr not in subStrs:
				# 	cnt += 1
				subStrs[subStr] = True
				subStr = subStr[1:]
			if char in subStr:
				i = subStr.index(char)
				subStr = subStr[i+1:]
			subStr += char

		if len(subStr) == k:
			subStrs[subStr] = True

		return len(subStrs)
```
```py
class Solution:
    """
    @param str: The string
    @param k: The length of the substring
    @return: The answer
    """
    def findSubstring(self, s, k):
        # Write your code here

        if k > 26:
            return 0

        d = {}
        ts = ""
        
        for i in range(len(s)):

            if len(ts) == k:
                d[ts] = True 
                ts = ts[1:]

            if s[i] in ts:
                j = ts.find(s[i])
                ts = ts[j+1:]

            ts += s[i]

        if len(ts) == k:
            d[ts] = True 

        return len(d)
        
```

### Official answer from lintcode

```py
class Solution:
    """
    @param str: The string
    @param k: The length of the substring
    @return: The answer
    """
    def check(self, str) :
        cnt = [ 0 for i in range(26) ]
        for i in str:
            cnt[ord(i) - ord('a')] += 1
            if(cnt[ord(i) - ord('a')] > 1):
                return False
        return True
    def findSubstring(self, str, k):
        # Write your code here
        
        if(k > 26):
            return 0
        ans = {}
        n = len(str)
        for i in range(0, n - k + 1):
            if(self.check(str[i:i + k])):
                ans[str[i:i + k]] = 1
        return len(ans)

```