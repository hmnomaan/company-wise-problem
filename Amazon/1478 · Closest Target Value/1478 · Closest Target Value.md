### 1478 · Closest Target Value
Algorithms
Easy
Accepted Rate
36%


### Description
Given an array, find two numbers in the array and their sum is closest to the target value but does not exceed the target value, return their sum.

## (i)
if there is no result meet the requirement, return -1.


## Example
```python
Input: target = 15 and array = [1,3,5,11,7]
Output: 14
Explanation: 
11+3=14

```
```python
Input: target = 16 and array = [1,3,5,11,7]
Output: 16
Explanation: 
11+5=16

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param target: the target
    @param array: an array
    @return: the closest value
    """
    def closest_target_value(self, target: int, array: List[int]) -> int:
        # Write your code here

```

### Tags
Two Pointers
## Company
Amazon

### Related Problems






### best answer
```py
from typing import (
    List,
)

class Solution:
    """
    @param target: the target
    @param array: an array
    @return: the closest value
    """
    def closest_target_value(self, target: int, array: List[int]) -> int:
        # Write your code here
        if not array or len(array) == 1:
            return -1
        
        array.sort()
        answer = float('-inf')
        left = 0
        right = len(array) - 1
        while left < right:
            if array[left] + array[right] < target:
                answer = max(answer, array[left] + array[right])
                left += 1
            elif array[left] + array[right] == target:
                return target
            else:
                right -= 1
        if answer == float('-inf'):
            return -1
        return answer
```
```py
class Solution:
    """
    @param target: the target
    @param array: an array
    @return: the closest value
    """
    def closestTargetValue(self, target, array):
        # Write your code here
        array.sort()
        start = 0 
        end = len(array) -1 
        curr_max = float('-inf')
        while start < end:
            temp_sum = array[start] + array[end] 
            if temp_sum > target:
                end -=1 
            else:
                start += 1 
                curr_max = max(curr_max, temp_sum)
        if curr_max ==  float('-inf'):
            return -1 
        else:
            return curr_max
```
```py
class Solution:
    """
    @param target: the target
    @param array: an array
    @return: the closest value
    """
    def closestTargetValue(self, target, array):
        # Write your code here
        l, r, = 0, len(array) - 1
        ans = -float('inf')
        array.sort()
        
        while l < r:
            s = array[l] + array[r]

            if s == target:
                return target
            if s < target:
                ans = max(ans, s)
                l += 1
            else:
                r -= 1
        
        return ans if ans!=-float('inf') else -1
```


### Official answer from lintcode
双指针
```py
class Solution:
    """
    @param target: the target
    @param array: an array
    @return: the closest value
    """
    def closestTargetValue(self, target, array):
        # Write your code here
        n = len(array)
        if n < 2:
            return -1
        array.sort()
        diff = 0x7fffffff
        left = 0
        right = n - 1
        while left < right:
            if array[left] + array[right] > target:
                right -= 1
            else:
                diff = min(diff, target - array[left] - array[right])
                left += 1
        if diff == 0x7fffffff:
            return -1
        else:
            return target - diff
```

//2
解题思路
题解代码
```py
from typing import (
    List,
)

class Solution:
    """
    @param target: the target
    @param array: an array
    @return: the closest value
    """
    def closest_target_value(self, target: int, array: List[int]) -> int:
        # Write your code here
        array.sort()
        left, right = 0, len(array)-1
        closest = float('-inf')
        while left < right:
            current = array[left] + array[right]
            if current <= target:
                if current > closest:
                    closest = current
                left += 1
            else:
                right -= 1
        return closest if closest > float('-inf') else -1
```