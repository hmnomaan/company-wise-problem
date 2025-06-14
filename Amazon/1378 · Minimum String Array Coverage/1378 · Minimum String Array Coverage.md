### 1378 · Minimum String Array Coverage
Algorithms
Medium
Accepted Rate
43%


### Description
Given a string collection tag_list, an array of strings all_tags, find the smallest all_tags sub-array contains all the string in the tag_list, output the length of this sub-array. If there is no return -1.

## (i)
1 <= |tag_list|,|all_tags| <=10000
All string length <= 50
String is not repeated in tag_list




## Example
```python
Input:  tag_list = ["made","in","china"], all_tags = ["made", "a","b","c","in", "china","made","b","c","d"]
Output: 3
Explanation:
["in", "china","made"] contains all the strings in tag_list,6 - 4 + 1 = 3.

```
```python
Input:  tag_list = ["a"], all_tags = ["b"]
Output: -1
Explanation:
Does not exist.

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param tag_list: The tag list.
    @param all_tags: All the tags.
    @return: Return the answer
    """
    def get_minimum_string_array(self, tag_list: List[str], all_tags: List[str]) -> int:
        # Write your code here

```

### Tags
Same Direction Two Pointers
Hash Table
Two Pointers

## Company
Amazon

### Related Problems






### best answer
```py
class Solution:
    """
    @param tagList: The tag list.
    @param allTags: All the tags.
    @return: Return the answer
    """
    def getMinimumStringArray(self, tagList, allTags):
        # Write your code here
        if not tagList or not allTags:
            return -1
        m, n = len(tagList), len(allTags)
        if m > n:
            return -1
        memo = {}
        for c in allTags:
           memo[c] = 0 
        
        for word in tagList:
            memo[word] = memo.get(word, 0) + 1
        
        res = n + 1
        l = 0
        cnt = 0
        for r in range(n):
            memo[allTags[r]] -= 1
            if memo[allTags[r]] >= 0:
                cnt += 1
            
            while l < r and cnt >= m:
                res = min(res, r - l + 1)
                memo[allTags[l]] += 1
                if memo[allTags[l]] > 0:
                    cnt -= 1
                l += 1
                    
        return res if res != n + 1 else -1
```
```py
import functools
import json

from typing import (
    List,
)

number = 0
txt = "\n"


def hook(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        global number, txt
        number += 1
        result = func(*args, **kwargs)
        txt += f"{func.__name__}->{number}->{args[1:]}->{result}\n"
        assert number < 8, txt
        return result
    return wrapper

class Solution:
    """
    @param tagList: The tag list.
    @param allTags: All the tags.
    @return: Return the answer
    """
    def getMinimumStringArray(self, tagList, allTags):
        # Write your code here
        mp1, mp2 = {}, {}
        for i in tagList:
            mp1[i] = 1
            mp2[i] = 0
        l , r = 0, -1
        n = len(allTags)
        m = len(tagList)
        cnt = 0
        ans = n + 1
        while(r < n):
            if(cnt < m):
                r += 1
                if(r == n):
                    break
                if(allTags[r]  in mp1):
                    mp2[allTags[r]] += 1
                    if(mp2[allTags[r]] == 1):
                        cnt += 1
            else:
                if(allTags[l] in mp1):
                    mp2[allTags[l]] -= 1
                    if(mp2[allTags[l]] == 0):
                        cnt -= 1
                l += 1
            if(cnt == m):
                ans = min(ans, r - l + 1)
        if(ans == n + 1):
            ans = -1
        return ans
```
```py
from typing import (
    List,
)

class Solution:
    """
    @param tag_list: The tag list.
    @param all_tags: All the tags.
    @return: Return the answer
    """
    def get_minimum_string_array(self, tag_list: List[str], all_tags: List[str]) -> int:
        counter = collections.Counter(tag_list)
        l, res, to_delete = 0, float('inf'), len(tag_list)
        for r, tag in enumerate(all_tags):
            if tag in counter:
                counter[tag] -= 1
                if counter[tag] >= 0:
                    to_delete -= 1
            while to_delete == 0:
                res = min(res, r - l + 1)
                if all_tags[l] in counter:  # 收缩窗口
                    counter[all_tags[l]] += 1
                    if counter[all_tags[l]] > 0:
                        to_delete += 1
                l += 1
        return res if res != float('inf') else -1

        

```

### Official answer from lintcode
Test point: Two pointers + HashSet Solution: Use Two pointers, the right pointer keeps moving to the right until it contains all the strings, use HashSet to maintain which strings appear in Two pointers, and move the left pointer once and update which strings appear in Two pointers. Time complexity O(n).
```py
class Solution:
    """
    @param tagList: The tag list.
    @param allTags: All the tags.
    @return: Return the answer
    """
    def getMinimumStringArray(self, tagList, allTags):
        # Write your code here
        mp1, mp2 = {}, {}
        for i in tagList:
            mp1[i] = 1
            mp2[i] = 0
        l , r = 0, -1
        n = len(allTags)
        m = len(tagList)
        cnt = 0
        ans = n + 1
        while(r < n):
            if(cnt < m):
                r += 1
                if(r == n):
                    break
                if(allTags[r]  in mp1):
                    mp2[allTags[r]] += 1
                    if(mp2[allTags[r]] == 1):
                        cnt += 1
            else:
                if(allTags[l] in mp1):
                    mp2[allTags[l]] -= 1
                    if(mp2[allTags[l]] == 0):
                        cnt -= 1
                l += 1
            if(cnt == m):
                ans = min(ans, r - l + 1)
        if(ans == n + 1):
            ans = -1
        return ans
```