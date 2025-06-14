### 1484 · The Most Frequent word

Algorithms
Medium
Accepted Rate
48%

### Description

Give a string s which represents the content of the novel, and then give a list indicating that the words do not participate in statistics, find the most frequent word(return the one with the smallest lexicographic order if there are more than one word)

## (i)
The length of s is not exceed 1000，the size of excludeWords is not exceed 20.

## Example

```python
Input: s = "Jimmy has an apple, it is on the table, he like it"，excludeWords = ["a","an","the"]
Output:"it"
Explanation:
"it" appears twice, the most frequently

```

```python
Input: s = "i have a a a a"，excludeWords = ["a"]
Output:"have"
Explanation:
"i" and "have" appear the same number of times, but have dictionary order is small

```

### SOLVE this:

```python
from typing import (
    Set,
)

class Solution:
    """
    @param s: a string
    @param excludewords: a dict
    @return: the most frequent word
    """
    def frequent_word(self, s: str, excludewords: Set[str]) -> str:
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
    @param excludewords: a dict
    @return: the most frequent word
    """
    def frequentWord(self, s, excludewords):
        # Write your code here
        
        dic = {}
        s_list = s.split(' ')
        s_list = [ i[:len(i)-1] if i[-1] == ',' or i[-1] == '.' else i for i in s_list  ]
        for i in s_list:
            if i in excludewords:
                continue
            if i not in dic:
                dic[i] = 0
            dic[i] +=1
            
        m = ''
        for i in dic.keys():
            m =  i 
            break
        if not m :
            return None
        for j in dic.keys():
            if dic[j]> dic[m] or dic[j] == dic[m] and j < m :
                m = j 
        return m
```
```py
class Solution:
    """
    @param s: a string
    @param excludewords: a dict
    @return: the most frequent word
    """
    def frequentWord(self, s, excludewords):
        # Write your code here
        s = s.split()
        for i in range(len(s)):
            if not s[i][-1].isalpha():
                s[i] = s[i][:-1]
        
        limit = set()
        for word in excludewords:
            limit.add(word)
            
        freq = 0    
        count = collections.Counter(s)
        for char in count:
            if count[char] > freq and char not in limit: 
                res = [char]
                freq = count[char]
            if count[char] == freq and char not in limit:
                res.append(char)
        res.sort()        
        return res[0]
```
```py
from typing import (
    Set,
)

class Solution:
    """
    @param s: a string
    @param excludewords: a dict
    @return: the most frequent word
    """
    def frequent_word(self, s: str, excludewords: Set[str]) -> str:
        s=s.replace(',', '')

        words = s.split(' ')

        hm = {}
        for word in words:
            if word not in excludewords:
                hm[word] = hm.get(word, 0) + 1
        
        for key in hm:
            res = key
            break 
        mx = hm[res]
        for key in hm:
            if hm[key] > hm[res]:
                res, mx = key, hm[key]
            elif hm[key] == hm[res] and key < res:
               
                res, mx = key, hm[key]
        return res 

```

### Official answer from lintcode
考点：

字典
正则表达式
题解：
本题利用python实现单词的截取，考虑正则表达式re.findall(r"\b\S+\b", s)。
tip:\b表示单词的开头或者结尾，\S表示非空白符任意字符，+表示前面字符可以重复一次以上，最后返回一个列表。
```py
import re
class Solution:
    """
    @param s: a string
    @param excludewords: a dict
    @return: the most frequent word
    """
    def frequentWord(self, s, excludewords):
        # Write your code here
        ans={}
        now=0
        s=" "+s
        lst = re.findall(r"\b\S+\b", s) 
        for x in lst:
            if x not in excludewords:
                if ans.__contains__(x) :
                    ans[x]+=1
                else :
                    ans[x]=1
                if ans[x]>now:
                    now=ans[x]
                    res=x
                elif ans[x]==now:
                    if x<res:
                        res=x
        return res
```
//2
n是s中含有单词数
O(nlogn) runtime. O(n) space. beats 100% submissions
```py
class Solution:
    """
    @param s: a string
    @param excludewords: a dict
    @return: the most frequent word
    """
    def frequentWord(self, s, excludewords):
        # Write your code here
        map = {}
        
        while len(s) > 0:
            end = s.find(' ') if s.find(' ') > -1 else len(s)
            word = s[:end] if s[end-1].isalpha() else s[:end-1]
            s = s[end+1:]
            if word not in excludewords:
                if word in map:
                    map[word] += 1 
                else:
                    map[word] = 1

        max = -1
        res = []
        for key, val in map.items():
            if val == max:
                res.append(key)
            elif val > max:
                max = val
                res = [key]
                
        res.sort()
        
        return res[0]
```
