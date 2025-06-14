### 1797 · optimalUtilization
Algorithms
Easy
Accepted Rate
32%


### Description
Give two sorted arrays. To take a number from each of the two arrays, the sum of the two numbers needs to be less than or equal to k, and you need to find the index combination with the largest sum of the two numbers. Returns a pair of indexes containing two arrays. If you have multiple index answers with equal sum of two numbers, you should choose the index pair with the smallest index of the first array. On this premise, you should choose the index pair with the smallest index of the second array.

1.The sum of the two numbers <= k
2.The sum is the biggest
3. Both array indexes are kept to a minimum
If you can not find a valid answer, please return a empty list [].
## (i)
You can assume that the numbers in arrays are all positive integer or zero.




## Example
```python
A = [1, 4, 6, 9], B = [1, 2, 3, 4], K = 9
return [2, 2]

```
```python
Input: 
A = [1, 4, 6, 8], B = [1, 2, 3, 5], K = 12
Output:
[2, 3]

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param a: a integer sorted array
    @param b: a integer sorted array
    @param k: a integer
    @return: return a pair of index
    """
    def optimal_utilization(self, a: List[int], b: List[int], k: int) -> List[int]:
        # write your code here

```

### Tags
Sort
Two Pointers
Array



## Company
Amazon

### Related Problems
56
Two Sum
Easy

533
Two Sum - Closest to target
Medium

607
Two Sum III - Data structure design
Easy

608
Two Sum II - Input array is sorted
Medium

610
Two Sum - Difference equals to target
Medium





### best answer
```py
from typing import (
    List,
)

class Solution:
    """
    @param a: a integer sorted array
    @param b: a integer sorted array
    @param k: a integer
    @return: return a pair of index
    """
    def optimal_utilization(self, a: List[int], b: List[int], k: int) -> List[int]:
        # write your code here
        #smalles index with largest sum
        pt1 = 0
        pt2 = 0
        max_sum = 0
        res = []
        #find the sum <k, collect all the index
        for i in range(len(a)):
            for j in range(len(b)):
                if a[i] + b[j] <= k:
                    if max_sum < a[i] + b[j]:
                        max_sum = a[i] + b[j]
                        res = []
                        res.append((i,j))
                    elif max_sum == a[i] + b[j]:
                        res.append((i,j))
        
        min_sum = float('inf')
        min_i_j = None
        sorted(res, key = lambda x:x[0])
        if len(res) ==0:
            return []
        return res[0]
        
                 
                


```
//2
```py
class Solution:
    """
    @param A: a integer sorted array
    @param B: a integer sorted array
    @param K: a integer
    @return: return a pair of index
    """
    def optimalUtilization(self, A, B, K):
        # write your code here
        r = len(B)-1
        max_ = -1
        loc = []
        for i in range(len(A)):
            while r>=0 and A[i]+B[r]>K and r>=0:
                r -= 1
            while r>=1 and B[r]==B[r-1]:
                r -= 1
            if r>=0 and A[i]+B[r]>max_:
                max_ = A[i]+B[r]
                loc = [i,r]
        return loc
```
//3
```py
class Solution:
    """
    @param A: a integer sorted array
    @param B: a integer sorted array
    @param K: a integer
    @return: return a pair of index
    """
    def optimalUtilization(self, A, B, K):
        # write your code here
        if not A or not B or K == 0:
            return []

        left, right = 0, len(B) - 1
        answer = [None, None]
        maxsum = 0 
        while left < len(A) and right >= 0:
            cursum = A[left] + B[right]
            if cursum == K:
                answer = [left, right]
                break        # 必须有break, 否则会超时
                
            elif cursum < K:
                if cursum > maxsum:
                    while right > 0 and B[right] == B[right - 1]:   # 这一步保证 B 数组取到下标最小的
                        right -= 1 
                    maxsum = A[left] + B[right]     # 更新 maxsum后，更新 answer 并移动指针
                    answer = [left, right]
                left += 1 

            else:
                right -= 1 
        
        return answer 

    '''
    整体思路:
        相向双指针
    
    创建left指针指向A数组的开头，创建right指针指向B数组的结尾。
        当A[left] + B[right] < K时: 记录left和right指针，left继续向有移动，
        当A[left] + B[right] > K的情况时：right向左移动，
        若相等: 则直接返回left和right
    
    注意:
        maxsum 记录当前最大和
        每次更新最大和后，更新answer 并移动指针 
    '''
```
//4
```py
class Solution:
    """
    @param A: a integer sorted array
    @param B: a integer sorted array
    @param K: a integer
    @return: return a pair of index
    """
    def optimalUtilization(self, A, B, K):

        answer = []
        len_A, len_B, index_A, index_B = len(A), len(B), 0, len(B) - 1
        if not A or not B or A[0] + B[0] > K:
            return []
        max_sum = A[0] + B[0] - 1
        while index_A < len_A and index_B >= 0:
            if A[index_A] + B[index_B] < K:
                if A[index_A] + B[index_B] > max_sum:
                    while index_B > 0 and B[index_B] == B[index_B - 1]:
                        index_B -= 1
                    max_sum = A[index_A] + B[index_B]
                    answer = [index_A, index_B]
                index_A += 1
            elif A[index_A] + B[index_B] > K:
                index_B -= 1
            else:
                answer = [index_A, index_B]
                break
        return answer

        # write your code here
```


### Official answer from lintcode
Algorithm: Opposing double pointers Solution Create a pointer to point to the beginning of array A, and create another pointer to point to the end of array B. When A[left] + B[right] < K, record the left and right pointers, and left continues to move forward. When A[left] + B[right] > K, right moves to the left. If they are equal, return left and right directly. If there are the same numbers in array B, no operation is performed, and right continues to move to the left. Complexity analysis Time complexity: O(n) n is the length of the array, and the entire array needs to be traversed. Space complexity: O(1) No additional space is required. Source code

```py
class Solution:
    """
    @param A: a integer sorted array
    @param B: a integer sorted array
    @param K: a integer
    @return: return a pair of index
    """
    def optimalUtilization(self, A, B, K):
        answer = []
        len_A, len_B, index_A, index_B = len(A), len(B), 0, len(B) - 1
        if not A or not B or A[0] + B[0] > K:
            return []
        max_sum = A[0] + B[0] - 1
        while index_A < len_A and index_B >= 0:
            if A[index_A] + B[index_B] < K:
                if A[index_A] + B[index_B] > max_sum:
                    while index_B > 0 and B[index_B] == B[index_B - 1]:
                        index_B -= 1
                    max_sum = A[index_A] + B[index_B]
                    answer = [index_A, index_B]
                index_A += 1
            elif A[index_A] + B[index_B] > K:
                index_B -= 1
            else:
                answer = [index_A, index_B]
                break
        return answer
```
//2
使用双指针算法，时间复杂度为O(n + m)
由于相等时返回的是A中小的index，所以A的指针从左往右，B的指针从右往左
```py
class Solution:
    """
    @param A: a integer sorted array
    @param B: a integer sorted array
    @param K: a integer
    @return: return a pair of index
    """
    def optimalUtilization(self, A, B, K):
        # write your code here
        if not A or not B:
            return []
        left, right = 0, len(B) - 1
        summ = A[0] + B[0]
        while left < len(A) and right >= 0:
            while (right >= 0 and A[left] + B[right] > K) or (right - 1 >= 0 and B[right] == B[right - 1]):
                right -= 1
            if A[left] + B[right] <= K:
                if A[left] + B[right] > summ:
                    summ = A[left] + B[right]
                    res = [left, right]
            left += 1
        return res
```
//3
解题思路
题解代码
```py
from typing import (
    List,
)

class Solution:
    """
    @param a: a integer sorted array
    @param b: a integer sorted array
    @param k: a integer
    @return: return a pair of index
    """
    def optimal_utilization(self, a: List[int], b: List[int], k: int) -> List[int]:
        # write your code here
        i = 0
        j =len(b)-1
        max_sum = float('-inf')
        max_indexes = []

        while i < len(a) and j >=0:
            s = a[i] + b[j]
            if s <= k and s > max_sum:
                max_sum = s
                while b[j]==b[j-1]:
                    j -=1
                max_indexes = [i, j]
            if s > k:
                j -= 1
            
            else:
                i += 1
                

        return max_indexes
```