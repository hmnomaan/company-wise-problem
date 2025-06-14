### 772 · Group Anagrams
Algorithms
Medium
Accepted Rate
70%



### Description

To give you a string array, please group the misplaced words(refers to the same character string with different permutations).

## (i) 
All inputs will be in lower-case.



## Example
```python
Input:
["eat","tea","tan","ate","nat","bat"]
Output:
[["ate","eat","tea"],
 ["bat"],
 ["nat","tan"]]

```
```python
Input:
["eat","nowhere"]
Output:
[["eat"],
 ["nowhere"]]

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param strs: the given array of strings
    @return: The anagrams which have been divided into groups
             we will sort your return value in output
    """
    def group_anagrams(self, strs: List[str]) -> List[List[str]]:
        # write your code here

```

### Tags
String
Sort
## Company
Bloomberg
Yelp
Amazon
Facebook
Uber

### Related Problems

171
Anagrams
Medium

922
Group Shifted Strings
Medium

503
Anagram (Map Reduce)
Medium

647
Find All Anagrams in a String
Medium

158
Valid Anagram
Easy

813
Find Anagram Mappings
Easy

773
Valid Anagrams
Easy





### best answer
```py

from typing import (
    List,
)

import collections
class Solution:
    """
    @param strs: the given array of strings
    @return: The anagrams which have been divided into groups
             we will sort your return value in output
    """
    def group_anagrams(self, strs: List[str]) -> List[List[str]]:
        mp = collections.defaultdict(list)

        for st in strs:
            key = "".join(sorted(st))
            mp[key].append(st)
        
        return list(mp.values())

```
```py
from typing import (
    List,
)

class Solution:
    """
    @param strs: the given array of strings
    @return: The anagrams which have been divided into groups
             we will sort your return value in output
    """
    def group_anagrams(self, strs: List[str]) -> List[List[str]]:
        # write your code here
        results = []
        s_sorted_2_order = {}
        order = 0
        for s in strs:
            s_sorted = ''.join(sorted(s))
            if s_sorted not in s_sorted_2_order:
                s_sorted_2_order[s_sorted] = order
                order += 1
                results.append([s])
            else:
                g_order = s_sorted_2_order[s_sorted]
                results[g_order].append(s)

        return results
```


### Official answer from lintcode
Solution idea: Sorting Two strings are anagrams of each other if and only if the two strings contain the same letters. The strings in the same group of anagrams have the same points, which can be used as the mark of a group of anagrams. A hash table is used to store each group of anagrams. The key of the hash table is the mark of a group of anagrams, and the value of the hash table is a list of a group of anagrams. Traverse each string, for each string, get the mark of the group of anagrams in which the string belongs, and add the current string to the list of the group of anagrams. After traversing all the strings, each key-value pair in the hash table is a group of anagrams. Since the two strings that are anagrams of each other contain the same letters, the strings obtained after sorting the two strings separately must be the same, so the sorted strings can be used as the keys of the hash table. Problem solution code
```py


from typing import (
    List,
)

import collections
class Solution:
    """
    @param strs: the given array of strings
    @return: The anagrams which have been divided into groups
             we will sort your return value in output
    """
    def group_anagrams(self, strs: List[str]) -> List[List[str]]:
        mp = collections.defaultdict(list)

        for st in strs:
            key = "".join(sorted(st))
            mp[key].append(st)
        
        return list(mp.values())

```