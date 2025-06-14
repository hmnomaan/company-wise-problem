### 608 · Two Sum II - Input array is sorted
Algorithms
Medium
Accepted Rate
65%


### Description
Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

##  (i)
You may assume that each input would have exactly one solution.

```python
from typing import (
    List,
)

class Solution:
    """
    @param nums: an array of Integer
    @param target: target = nums[index1] + nums[index2]
    @return: [index1 + 1, index2 + 1] (index1 < index2)
    """
    def two_sum(self, nums: List[int], target: int) -> List[int]:
        # write your code here

```


## Example
Example 1:
```py
Input: nums = [2, 7, 11, 15], target = 9 
Output: [1, 2]
```
Example 2:

```py
Input: nums = [2,3], target = 5
Output: [1, 2]
```


### Tags
Opposite Direction Two Pointers
Hash Table
Two Pointers


## Company
Amazon

### Related Problems
1879
Two Sum VII
Hard

587
Two Sum - Unique pairs
Medium

607
Two Sum III - Data structure design
Easy

689
Two Sum IV - Input is a BST
Medium

610
Two Sum - Difference equals to target
Medium

533
Two Sum - Closest to target
Medium

1797
optimalUtilization
Easy

1796
K-Difference
Medium

443
Two Sum - Greater than target
Medium

56
Two Sum
Easy

609
Two Sum - Less than or equal to target
Medium




### best answer
```py
from typing import (
    List,
)

class Solution:
    """
    @param nums: an array of Integer
    @param target: target = nums[index1] + nums[index2]
    @return: [index1 + 1, index2 + 1] (index1 < index2)
    """
    # 1. nested loop
    # n**2, 1 
    # 2. two pointers
    # n, 1
    def two_sum(self, nums: List[int], target: int) -> List[int]:

        left, right = 0, len(nums)-1
        while left < right:
            cur_sum = nums[left] + nums[right]
            if cur_sum == target:
                return [left+1, right+1]
            if cur_sum < target:
                left += 1
                continue
            if cur_sum > target:
                right -= 1
                continue
        
        return [-1, -1]
```


### Official answer from lintcode
Use the double pointer method. Keep moving the left pointer and adjusting the position of the right pointer until they are equal.
```py
class Solution:
    """
    @param nums {int[]} n array of Integer
    @param target {int} = nums[index1] + nums[index2]
    @return {int[]} [index1 + 1, index2 + 1] (index1 < index2)
    """
    def twoSum(self, nums, target):
        # Write your code here
        l, r = 0, len(nums)-1
        while l < r:
            value = nums[l] + nums[r]
            if value == target:
                return [l+1, r+1]
            elif value < target:
                l += 1
            else:
                r -= 1
        return []
```