### 679 · Unique Paths III
Algorithms
Hard
Accepted Rate
42%


### Description

Follow up for "Unique Paths II": http://lintcode.com/en/problem/unique-paths-ii/

Now each grid contains a value, so each path also has a value. Find the sum of all the unique values paths.



## Example
1
```python
Input:
[
  [1,1,2],
  [1,2,3],
  [3,2,4]
]
Output:
21
Explanation:
There are 2 unique value path:
[1,1,2,3,4] = 11
[1,1,2,2,4] = 10

```
2
```python
Input:
[
    [1,5],
    [4,6]
]
Output: 23
Explanation:
There are 2 unique value path:
[1,5,6] = 12
[1,4,6] = 11

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param grid: an array of arrays
    @return: the sum of all unique weighted paths
    """
    def unique_weighted_paths(self, grid: List[List[int]]) -> int:
        # write your codes here

```

### Tags
Dynamic Programming/DP
Memoization Search
Coordinate DP



## Company
Amazon

### Related Problems

114
Unique Paths
Easy

115
Unique Paths II
Easy

795
4-Way Unique Paths
Medium




### best answer
```py
class Solution:
    """
    @param: : an array of arrays
    @return: the sum of all unique weighted paths
    """

    def uniqueWeightedPaths(self, grid):
        # write your codes here
        n=len(grid)
        m=len(grid[0])
        if n == 0 or m == 0:
            return 0
        s=[[set() for _ in range(m)] for __ in range(n)]
        s[0][0].add(grid[0][0])
        for i in range(n):
            for j in range(m):
                if i==0 and j==0:
                    s[i][j].add(grid[i][j])
                else:
                    for val in s[i-1][j]:
                        s[i][j].add(val+grid[i][j])
                    for val in s[i][j-1]:
                        s[i][j].add(val+grid[i][j])
        ans=0
        for val in s[-1][-1]:
            ans+=val
        return ans
```


### Official answer from lintcode

```py
# 记忆化搜索

class Solution:
    """
    @param: : an array of arrays
    @return: the sum of all unique weighted paths
    """
    
    def uniqueWeightedPaths(self, grid):
        # write your codes here
        if not grid:
            return 0
        return sum(self.helper(0, 0, grid, {}))
    
    def helper(self, i, j, grid, memo):
        if i >= len(grid) or j >= len(grid[0]):
            return set()
            
        if i == len(grid) - 1 and j == len(grid[0]) - 1:
            return set([grid[i][j]])
            
        if (i, j) in memo:
            return memo[(i, j)]
            
        down = self.helper(i + 1, j, grid, memo)
        right = self.helper(i, j + 1, grid, memo)
        
        ans = set([(obj + grid[i][j]) for obj in down.union(right)])
        
        memo[(i, j)] = ans
        return ans

# 滚动数组DP    
    

class Solution:
    """
    @param: : an array of arrays
    @return: the sum of all unique weighted paths
    """
    
    def uniqueWeightedPaths(self, grid):
        # write your codes here
        if not grid or not grid[0]:
            return 0
            
        dp = [set() for i in range(len(grid[0]))]
        dp[len(grid[0]) - 1].add(0)
        
        for row in range(len(grid) - 1, -1, -1):
            for col in range(len(grid[0]) - 1, -1, -1):
                if col + 1 < len(grid[0]):
                    dp[col] = dp[col].union(dp[col + 1])
                dp[col] = set([(obj + grid[row][col]) for obj in dp[col]])
                
        return sum(dp[0])
```