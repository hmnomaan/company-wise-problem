### 1480 · Dot Product
Algorithms
Easy
Accepted Rate
58%


### Description
Given two array, output their dot product [https://en.wikipedia.org/wiki/Dot_product]

## (i)

if there is no dot product, return -1.


## Example
1
```python
Input: A = [1,1,1] and B = [2,2,2]
Output: 6
Explanation:
1*2+1*2+1*2=6

```
2
```python
Input: A = [3,2] and B = [2,3,3]
Output: -1
Explanation:
there is no dot product

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param a: an array
    @param b: an array
    @return: dot product of two array
    """
    def dot_product(self, a: List[int], b: List[int]) -> int:
        # Write your code here

```

### Tags

## Company
Facebook
Amazon

### Related Problems






### best answer
//1
```py
from typing import (
    List,
)

class Solution:
    """
    @param a: an array
    @param b: an array
    @return: dot product of two array
    """
    def dot_product(self, a: List[int], b: List[int]) -> int:
        # Write your code here
        if len(a)==0 or len(b)==0 or len(a)!=len(b):
            return -1
        ans=0
        for i,x in enumerate(a):
            ans+=x*b[i]
        return ans

```
//2
```py
class Solution:
    """
    @param A: an array
    @param B: an array
    @return: dot product of two array
    """
    def dotProduct(self, A, B):
        if len(A) != len(B) or not A:
            return -1
        
        result = 0            
        for i in range(len(A)):
            result += A[i] * B[i]
            
        return result
```
//3
```py
class Solution:
    """
    @param A: an array
    @param B: an array
    @return: dot product of two array
    """
    def dotProduct(self, A, B):
        # Write your code here
        if len(A) != len(B) or A == [] or B==[]:
            return -1
        result = 0
        for i in range(len(A)):
            result += A[i]*B[i]
        return result
```
//4
```py
class Solution:
    """
    @param A: an array
    @param B: an array
    @return: dot product of two array
    """
    def dotProduct(self, A, B):
        # Write your code here
        
        if not A or not B or len(A) != len(B):
            return -1
        
        return sum(a * b for a, b in zip(A, B))
```

### Official answer from lintcode
1
```py
class Solution:
    """
    @param A: an array
    @param B: an array
    @return: dot product of two array
    """
    def dotProduct(self, A, B):
        # Write your code here
        if len(A) == 0 or len(B) == 0 or len(A) != len(B):
            return -1
        ans = 0
        n = len(A)
        for i in range(n):
            ans += A[i] * B[i]
        return ans
```
//2
娱乐一行😇

题解代码
```py
class Solution:
    """
    @param A: an array
    @param B: an array
    @return: dot product of two array
    """
    def dotProduct(self, A, B):
        # Write your code here
        return -1 if not A or not B or len(A) != len(B) else sum([i * j for i, j in zip(A, B)])
```