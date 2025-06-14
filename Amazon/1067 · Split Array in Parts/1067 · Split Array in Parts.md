### 1067 · Split Array in Parts
Algorithms
Medium
Accepted Rate 


### Description
Given a (singly) array with head node root, write a function to split the array into k consecutive array "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input array, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a array of Array's representing the array parts that are formed

## (i)
The length of root will be in the range [0, 1000].
Each value of a node in the input will be an integer in the range [0, 999].
k will be an integer in the range [1, 50].


## Example
```python
Input: 
root = [1, 2, 3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The input and each element of the output are array of array.

```
```python
Input: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param root: the list
    @param k: the split sum
    @return: the answer
    """
    def split_linked_listin_parts(self, root: List[int], k: int) -> List[List[int]]:
        # Write your code here.

```

### Tags
Array
## Company
Amazon

### Related Problems






### best answer
```py
class Solution:
    """
    @param root: the list
    @param k: the split sum
    @return: the answer
    """
    def splitLinkedListinParts(self, root, k):
        # Write your code here.
        if k == len(root):
            return root 
        
        part = len(root) // k 
        
        remain = len(root) % k 
        partition = [part] * k 
        
        for i in range(remain):
            partition[i] += 1 
        
        res = []
        s = root
        for number in partition:
            res.append(s[:number])
            s = s[number :]
        
        
        return res
```
```py
class Solution:
    """
    @param root: the list
    @param k: the split sum
    @return: the answer
    """
    def splitLinkedListinParts(self, root, k):
        # Write your code here.
        result = []
        size, remainder = divmod(len(root), k)
        start = 0
        for i in range(k):
            end = start + size + (1 if remainder > 0 else 0)
            result.append( root[start:end] )
            start = end
            remainder -= 1
        return result
            

        # length = 0
        # head = root
        # while head:
        #     length += 1
        #     head = head.next
            
        # size, remainder = divmod(length, k)
        # result = []
        
        # head = root
        # for i in range(k):
        #     start = head
        #     for j in range(size-1):
        #         head = head.next
        #     if remainder:
        #         head = head.next
        #         remainder -= 1
        #     result.append(start)
            
        #     if head:
        #         n = head.next
        #         head.next = None
        #         start = n
            
        # return result
```

### Official answer from lintcode
先获取数组长度，将数组长度n与k整除后的余数sum，前sum个部分长度为n / k + 1，后面的每个部分的长度为n / k
```py
class Solution:
    """
    @param root: the list
    @param k: the split sum
    @return: the answer
    """
    def splitLinkedListinParts(self, root, k):
        # Write your code here.
        res = [];
        length = len(root);
        parts = length / k;
        mod = length % k;
        temp = 0;
        for i in range(0, k):
            if i < mod:
                res.append(root[temp : temp + parts + 1])
                temp = temp + parts + 1
            else:
                res.append(root[temp : temp + parts])
                temp = temp + parts
        return res
```