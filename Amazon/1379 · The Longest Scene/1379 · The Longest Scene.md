### 1379 · The Longest Scene
Algorithms
Hard
Accepted Rate
59%



### Description
A string, each character representing a scene. Between two identical characters is considered to be a continuous scene. For example: abcda, you can think of these five characters as the same scene. Or acafghbeb can think of two aca and beb scenes. If there is a coincidence between the scenes, then the scenes are combined. For example, abcab, where abca and bcab are coincident, then the five characters are considered to be the same scene. Give a string to find the longest scene.

## (i) 
1 <= |str| <=1e5
str contains only lowercase letters


## Example
```python
Input: "abcda"
Output: 5
Explanation:
The longest scene is "abcda".

```
```python
Input: "abcab"
Output: 5
Explanation:
The longest scene is "abcab".

```
### SOLVE this:

```python
class Solution:
    """
    @param str: The scene string
    @return: Return the length longest scene
    """
    def get_longest_scene(self, str: str) -> int:
        # Write your code here

```

### Tags
Sweep Line


## Company
Amazon

### Related Problems






### best answer
1
```py
class Solution:
    """
    @param str: The scene string
    @return: Return the length longest scene
    """
    def getLongestScene(self, str):
        # 记录每个字符的左端点和右端点，相等于求若干线段合并后最长线段长度，
        # 使用扫描线即可。时间复杂度O(n)
        if not str:
            return 0
        
        pos = {}
        
        for i in range(len(str)):
            char = str[i]
            if char not in pos:
                # [left_pos, right_pos]
                pos[char] = [i, i]
            else:
                pos[char][1] = i

        intervals = sorted(pos.values(), key = lambda x: x[0])
        stack = []
        max_l = 0
        
        for left, right in intervals:
            if not stack or stack[-1][1] < left:
                stack.append([left, right])
            else:
                stack[-1][1] = max(stack[-1][1], right)
            
            max_l = max(max_l, stack[-1][1] - stack[-1][0] + 1)
        
        return max_l
```
2
```py
class Solution:
    """
    @param str: The scene string
    @return: Return the length longest scene
    """
    def getLongestScene(self, str):
        # Write your code here
        table = {}
        for i in range(len(str)):
            c = str[i]
            if c not in table:
                table[c] = [i, i]
            else:
                table[c][1] = i
        
        arr = []
        for c in str:
            if c in table:
                arr.append(table[c])
                del table[c]
        ans = 0
        lasts = laste = -1
        for s, e in arr:
            if laste < s:
                ans = max(ans, laste - lasts + 1)
                lasts = s
                laste = e
            else:
                laste = max(laste, e)
        ans = max(ans, laste - lasts + 1)
        return ans
```

3
```py
class Solution:
    """
    @param str: The scene string
    @return: Return the length longest scene
    """
    def getLongestScene(self, s):
        if not s or len(s) == 0:
            return 0
        n = len(s)
        dic = {}
        for i, c in enumerate(s):
            if c not in dic:
                dic[c] = [i, i]
            else:
                dic[c][1] = i
        indegree = collections.defaultdict(int)
        for c in dic:
            s, e = dic[c][0], dic[c][1]
            indegree[s] += 1
            indegree[e] -= 1
        curr = ans = 0
        for t in sorted(indegree):
            if curr == 0:
                start = t
            curr += indegree[t]
            if curr == 0:
                end = t
                ans = max(ans, end - start + 1)
        return ans
```


### Official answer from lintcode
Test point: Scan line Solution: Recording the left and right endpoints of each character is equivalent to finding the longest line segment length after several line segments are combined. Scan line can be used. Time complexity O(n)
```py
class Solution:
    """
    @param str: The scene string
    @return: Return the length longest scene
    """
    def getLongestScene(self, str):
        # Write your code here
        seg = []
        print(Point())
        p = Point()
        for i in range(26):
            p.x = len(str)
            p.y = -1
            seg.append(p)
        for i in range(len(str)):
            t = ord(str[i]) - ord('a')
            seg[t].x = min(seg[t].x, i)
            seg[t].y = max(seg[t].y, i)
        seg.sort()
        maxlen = seg[0].y - seg[0].x + 1
        posl, posr = seg[0].x, seg[0].y
        ans = maxlen
        for i in range(1, 26):
            if (seg[i].x < len(str) and seg[i].y >= 0) :
                if (seg[i].x <= posr):
                    posr = max(posr, seg[i].y)
                else:
                    posl = seg[i].x
                    posr = seg[i].y
                ans = max(ans, posr - posl + 1)
        return ans
```
---------------------------------------------------------------
---------------------------------------------------------------
Solution
 Difference array + scan line 
 Solution code
```py
from collections import *#defaultdict, Counter, deque
class Solution:
    def get_longest_scene(self, s: str) -> int:
        d=defaultdict(list)
        n=len(s)
        for i,c in enumerate(s):
            d[c].append(i)

        diff=[0]*(n+1)
        for k in sorted(d.keys()):
            start,end=d[k][0],d[k][-1]
            diff[start]+=1
            diff[end]-=1
        tmp,count=0,1
        ans=0
        for i in range(n+1):
            tmp+=diff[i]
            if tmp!=0:
                count+=1
            else :
                count=1
            ans=max(ans,count)
        return ans
```