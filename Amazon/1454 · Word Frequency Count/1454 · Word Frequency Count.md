### 1454 · Word Frequency Count
Algorithms
Medium
Accepted Rate
39%



### Description
Input a string s and a string list excludeList to find all the most frequent words in s that do not exist in excludeList. Your results will be sorted by lexicographic order by online judge.

### (i)
The words are case-insensitive and finally return lowercase words
Non-alphabetic characters in the string are considered as spaces, and spaces are word separators
The length of all words does not exceed 
1
0
5
10 
5
  and the length a word does not exceed 
100
100




## Example
1
```python
Input：s="I love Amazon.", excludeList=[] 
Output：["i","love","amazon"]
Explanation:
"i", "love", and "amazon" are the words that appear the most.

```
2
```python
Input：s="Do not trouble trouble.", excludeList=["do"]
Output：["trouble"]
Explanation:
"trouble" is the most frequently occurring word.

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param s: The string s
    @param exclude_list: The excludeList
    @return: Return the most frequent words
             we will sort your return value in output
    """
    def get_words(self, s: str, exclude_list: List[str]) -> List[str]:
        # Write your code here

```

### Tags
Hash Table
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
import re

class Solution:
    """
    @param s: The string s
    @param exclude_list: The excludeList
    @return: Return the most frequent words
             we will sort your return value in output
    """
    def get_words(self, s: str, exclude_list: List[str]) -> List[str]:
        # Write your code here
        exclude = set(word.lower() for word in exclude_list)
        s = re.sub(r'[^a-zA-Z]', ' ', s).lower()
        words = s.split()
        d = collections.defaultdict(int)
        max_freq = 0
        res = []
        for word in words:
            if word not in exclude:
                d[word] += 1
                max_freq = max(max_freq, d[word])
        for key in d:
            if d[key] == max_freq:
                res.append(key)
        return res
```
2
```py
from typing import (
    List,
)

from collections import Counter
import re

class Solution:
    """
    @param s: The string s
    @param exclude_list: The excludeList
    @return: Return the most frequent words
             we will sort your return value in output
    """
    def get_words(self, s: str, exclude_list: List[str]) -> List[str]:
        # Write your code here
        s = s.lower()
        s = re.sub(r'[^a-z]+', ' ', s)
        s=s.split()
        freqs=Counter(s)
        for word in exclude_list:
            if word in freqs:
                del freqs[word]
        mostFrequent=max(freqs.values())
        return [k for k,v in freqs.items() if v==mostFrequent]
```
3
```py
from typing import (
    List,
)

class Solution:
    """
    @param s: The string s
    @param exclude_list: The excludeList
    @return: Return the most frequent words
             we will sort your return value in output
    """
    def get_words(self, s: str, exclude_list: List[str]) -> List[str]:
        # Write your code here
        # split s into words
        s = s.lower()
        words = []
        word = ""
        for letter in s:
            if letter >= "a" and letter <= "z":
                word += letter
            else:
                if word != "":
                    words.append(word)
                word = ""
        if word != "":
            words.append(word)

        # count freq of words: dict<word:freq>
        word_to_freq = dict()
        for word in words:
            if word not in word_to_freq:
                word_to_freq[word] = 1
            else:
                word_to_freq[word] += 1

        # get unique exclude list: set(exclude_words)
        excluded_words = set()
        for word in exclude_list:
            excluded_words.add(word.lower())

        # loop through dict<word:freq> (if not excluded)
            # keep cur_max, if cur_freq > cur_max: reset ans
            # if cur_freq = cur_max: append ans
        cur_max = 0
        ans = []
        for word, freq in word_to_freq.items():
            if word in excluded_words:
                continue
            
            if freq > cur_max:
                cur_max = freq
                ans = [word]
            elif freq == cur_max:
                ans.append(word)
        return ans

```


### Official answer from lintcode
考点

字典
题解
先对字符串 s 进行分词，之后通过 字典 统计单词的词频，最终输出词频最高的单词。
```py
class Solution:
    """
    @param s: The string s
    @param excludeList: The excludeList
    @return: Return the most frequent words
    """

    def getWords(self, s, excludeList):
        s = s.lower()
        words = []
        p = ''
        for letter in s:
            if letter < 'a' or letter > 'z':
                if p != '':
                    words.append(p)
                p = ''
            else:
                p += letter
        if p != '':
            words.append(p)
        dic = {}
        for word in words:
            word = word.lower()
            if dic.has_key(word):
                dic[word] += 1
            else:
                dic[word] = 1
        dic2 = {}
        for word in excludeList:
            word = word.lower()
            if dic2.has_key(word):
                dic2[word] += 1
            else:
                dic2[word] = 1
        ans = []
        mx = 0
        for word in words:
            word = word.lower()
            if not dic2.has_key(word):
                if dic[word] > mx:
                    mx = dic[word]
                    ans = [word]
                elif dic[word] == mx and word not in ans:
                    ans.append(word)
        return ans
```
//2
Python solution with string.punctuation
```py
import string
from collections import defaultdict
class Solution:
    """
    @param s: The string s
    @param excludeList: The excludeList
    @return: Return the most frequent words
    """
    def getWords(self, s, excludeList):
        # Write your code here
        exclu = set()
        dic = defaultdict(int)
        res = []
        for i in excludeList:
            exclu.add(i.lower())
        sList = [i.strip(string.punctuation) for i in s.split()]
        for i in sList:
            word = i.lower()
            if word not in exclu:
                dic[word] += 1
        dic_sorted = sorted(dic.items(), key = lambda x: x[1])
        fre = dic_sorted[-1][1]
        for i in reversed(dic_sorted):
            if i[1] < fre:
                break
            # print(i)
            res.append(i[0])
        return res

```