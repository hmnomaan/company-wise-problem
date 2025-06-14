### 1798 · Minimum Cost to Merge Stones
Algorithms
Hard
Accepted Rate
50%



### Description
There are N piles of stones arranged in a row. The i-th pile has stones[i] stones.

A move consists of merging exactly K consecutive piles into one pile, and the cost of this move is equal to the total number of stones in these K piles.

Find the minimum cost to merge all piles of stones into one pile. If it is impossible, return -1.

## (i)
1 <= stones.length <= 100
2 <= K <= 30
1 <= stones[i] <= 100


## Example
```python
Input: stones = [3,2,4,1], K = 2
Output: 20
Explanation: 
We start with [3, 2, 4, 1].
We merge [3, 2] for a cost of 5, and we are left with [5, 4, 1].
We merge [4, 1] for a cost of 5, and we are left with [5, 5].
We merge [5, 5] for a cost of 10, and we are left with [10].
The total cost was 20, and this is the minimum possible.

```
```python
Input: stones = [3,2,4,1], K = 3
Output: -1
Explanation: After any merge operation, there are 2 piles left, and we can't merge anymore.  So the task is impossible.

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param stones: 
    @param k: 
    @return: return a integer 
    """
    def merge_stones(self, stones: List[int], k: int) -> int:
        # write your code here

```

### Tags
Interval DP
Dynamic Programming/DP
## Company
Amazon

### Related Problems
1384
Segment Stones Merge
Super





### best answer
```py
class Solution:
    def mergeStones(self, stones, K):
        n = len(stones)
        if (n - 1) % (K - 1) != 0:
            return -1
        preSum = [0] * (n + 1)
        for i in range(n):
            preSum[i + 1] = preSum[i] + stones[i]
        dp = [[0] * n for _ in range(n)]
        for length in range(K, n + 1):
            for i in range(0, n - length + 1):
                j = i + length - 1
                dp[i][j] = min(dp[i][k] + dp[k + 1][j] for k in range(i, j, K - 1))
                if (j - i) % (K - 1) == 0:
                    dp[i][j] += preSum[j + 1] - preSum[i]
        return dp[0][n - 1]
```
```py
class Solution:
    """
    @param stones: 
    @param K: 
    @return: return a integer 
    """
    def mergeStones(self, stones, K):
        n = len(stones)
        if (n-1) % (K-1): return -1
        sums = [0] * (n+1)
        for i in range(n):
            sums[i+1] = sums[i] + stones[i]
        dp = [ [0] * n for _ in range(n) ]
        for k in range(1,n):
            for l in range(n):
                if l + k >= n:break
                r = l + k
                dp[l][r] = min( dp[l][i] + dp[i+1][r] for i in range(l,r,K-1) )
                if (r - l) % (K - 1) == 0: dp[l][r] += sums[r+1] - sums[l] 
        return dp[0][n-1]
```
```py
from typing import (
    List,
)
from itertools import accumulate
class Solution:
    """
    @param stones: 
    @param k: 
    @return: return a integer 
    """
    def merge_stones(self, stones: List[int], k: int) -> int:
        # write your code here
        n = len(stones)

        if (n-1)%(k-1):
            return -1

        accu = [0] + list(accumulate(stones))

        dp = [[0]*n for _ in range(n)]

        for length in range(k, n+1):

            for i in range(n - length + 1):
                j = i + length - 1

                dp[i][j] = min( dp[i][mid] + dp[mid+1][j] for mid in range(i,j,k-1) )

                if (length-1)%(k-1) == 0:
                    dp[i][j] += accu[j+1] - accu[i]


        return dp[0][n-1]
```


### Official answer from lintcode
f[i][j] 表示下标i到j合并的最小花费。
能合併时((j - i) % (K - 1) == 0)就合併，所以f[i][j]加上下标i到j区间合。
下标区间小于K时(j - i + 1 < K)无法合併，f[i][j]为0。
```py
class Solution:
    """
    @param stones: 
    @param K: 
    @return: return a integer 
    """
    def mergeStones(self, stones, K):
        n = len(stones)
        
        if (n - 1) % (K - 1) != 0:
            return -1
        
        f = [[0 for _ in range(n)] for _ in range(n)]
        
        prefix = [0 for _ in range(n + 1)]
        for i in range(n):
            prefix[i + 1] = prefix[i] + stones[i]
            
        for l in range(K, n + 1):
            for i in range(n - l + 1):
                j = i + l - 1
                f[i][j] = sys.maxsize
                for m in range(i, j, K - 1):
                    f[i][j] = min(f[i][j], f[i][m] + f[m + 1][j])
                if (j - i) % (K - 1) == 0:
                    f[i][j] += prefix[j + 1] - prefix[i]
        
        return f[0][n - 1]
```
```py
class Solution:
    """
    @param stones: 
    @param K: 
    @return: return a integer 
    """
    def mergeStones(self, stones, K):
        n = len(stones)
        
        if (n - 1) % (K - 1) != 0:
            return -1
        
        # preprocessing
        prefix_sum = self.get_prefix_sum(stones)
        
        # state: dp[i][j][k] i到j这一段合并为 k 堆石子的最小代价
        dp = [[
            [float('inf')] * (K + 1)
            for _ in range(n)
        ] for __ in range(n)]
        
        # initialization: 一开始所有石子各自为一堆，代价为 0
        for i in range(n):
            dp[i][i][1] = 0
        
        # function:
        # dp[i][j][k] = min{dp[i][x][k - 1] + dp[x + 1][j][1]} // for k > 1
        # dp[i][j][1] = dp[i][j][K] + sum(stones[i..j]) // for k = 1
        for i in range(n - 2, -1, -1):
            for j in range(i + 1, n):
                for k in range(2, K + 1):
                    for x in range(i, j):
                        dp[i][j][k] = min(dp[i][j][k], dp[i][x][k - 1] + dp[x + 1][j][1])
                dp[i][j][1] = dp[i][j][K] + prefix_sum[j + 1] - prefix_sum[i]
        
        # answer: dp[0][n - 1][1]
        return -1 if dp[0][n - 1][1] == float('inf') else dp[0][n - 1][1]
        
    def get_prefix_sum(self, A):
        prefix_sum = [0]
        for a in A:
            prefix_sum.append(prefix_sum[-1] + a)
        return prefix_sum
```
///
解题思路
这个题的思路不太容易。
状态数组f[i][j][k]表示将stones[i..j]分成k堆所需要的最小花费。
当k >= 2时，需要分作两步：左边1堆，右边k-1堆。（左边的1堆有点小技巧，要么含有1个元素，要么含有1+(K-1)个元素，要么1+(K-1)+(K-1)个元素，所以每次的步长不是1，而是K-1）
当k==1时，需要先把整段分成K堆，然后合成1堆。
由此，上面的计算顺序是先2到K堆，最后是1堆。

题解代码
```py
class Solution:
    """
    @param stones: 
    @param K: 
    @return: return a integer 
    """
    def mergeStones(self, stones, K):
        # write your code here
        n = len(stones)
        if (n - 1) % (K - 1) != 0:
            return -1

        presum = [0]
        for stone in stones:
            presum.append(presum[-1] + stone)

        # f[i][j][k]: min cost for merging stones[i..j] to k piles
        f = [[[float('inf') for k in range(K + 1)] for j in range(n)] for i in range(n)]
        for i in range(n):
            f[i][i][1] = 0

        for length in range(2, n + 1):
            for i in range(0, n - length + 1):
                j = i + length - 1
                for k in range(2, K + 1):
                    for m in range(i, j, K - 1):
                        f[i][j][k] = min(f[i][j][k], f[i][m][1] + f[m + 1][j][k - 1])
                f[i][j][1] = f[i][j][K] + presum[j + 1] - presum[i]

        return f[0][n - 1][1]
```