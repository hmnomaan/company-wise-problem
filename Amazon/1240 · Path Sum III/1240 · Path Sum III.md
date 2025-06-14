### 1240 · Path Sum III
Algorithms
Easy
Accepted Rate
70%
 


### Description
You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.




## Example
```python
Input：root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8
Output：3
Explanation：
      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11

```
```python
Input：root = [11,6,-3], sum = 17
Output：1
Explanation：
      11
     /  \
    6   -3
Return 17. The path that sum to 17 is:

1.  11 -> 6

```
### SOLVE this:

```python
from lintcode import (
    TreeNode,
)

"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: 
    @param sum: 
    @return: 
    """
    def path_sum(self, root: TreeNode, sum: int) -> int:
        # 

```

### Tags
Depth First Search/DFS

## Company
Amazon
Facebook
Quora
Uber

### Related Problems






### best answer
```py
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: 
    @param sum: 
    @return: the num of sum path
    """
    def pathSum(self, root, sum):
        # write your code here
        if not root:
            return 0
            
        self.count = 0
        self.dfs(root, sum, [root.val])
        
        return self.count
        
    def dfs(self, node, target, path):
        
        s = 0
        for i in range(len(path)-1, -1, -1):
            s += path[i]
            if s == target:
                self.count += 1
        
        if node.left:
            self.dfs(node.left, target, path+[node.left.val])
        if node.right:
            self.dfs(node.right, target, path+[node.right.val])
            
```


### Official answer from lintcode
前缀和
思路与算法

我们仔细思考一下，解法一中应该存在许多重复计算。我们定义节点的前缀和为：由根结点到当前结点的路径上所有节点的和。我们利用先序遍历二叉树，记录下根节点 
root
root 到当前节点 
p
p 的路径上除当前节点以外所有节点的前缀和，在已保存的路径前缀和中查找是否存在前缀和刚好等于当前节点到根节点的前缀和 
c
u
r
r
curr 减去 
targetSum
targetSum。

对于空路径我们也需要保存预先处理一下，此时因为空路径不经过任何节点，因此它的前缀和为 
0
0。

假设根节点为 
root
root，我们当前刚好访问节点 
node
node，则此时从根节点 
root
root 到节点 
node
node 的路径（无重复节点）刚好为 
root
→
p
1
→
p
2
→
…
→
p
k
→
node
root→p 
1
​
 →p 
2
​
 →…→p 
k
​
 →node，此时我们可以已经保存了节点 
p
1
,
p
2
,
p
3
,
…
,
p
k
p 
1
​
 ,p 
2
​
 ,p 
3
​
 ,…,p 
k
​
  的前缀和，并且计算出了节点 
node
node 的前缀和。

假设当前从根节点 
root
root 到节点 
node
node 的前缀和为 
curr
curr，则此时我们在已保存的前缀和查找是否存在前缀和刚好等于 
curr
−
targetSum
curr−targetSum。假设从根节点 
root
root 到节点 
node
node 的路径中存在节点 
p
i
p 
i
​
  到根节点 
root
root 的前缀和为 
curr
−
targetSum
curr−targetSum，则节点 
p
i
+
1
p 
i+1
​
  到 
node
node 的路径上所有节点的和一定为 
targetSum
targetSum。

我们利用深度搜索遍历树，当我们退出当前节点时，我们需要及时更新已经保存的前缀和。

代码
```py
class Solution:
    def pathSum(self, root: TreeNode, targetSum: int) -> int:
        prefix = collections.defaultdict(int)
        prefix[0] = 1

        def dfs(root, curr):
            if not root:
                return 0
            
            ret = 0
            curr += root.val
            ret += prefix[curr - targetSum]
            prefix[curr] += 1
            ret += dfs(root.left, curr)
            ret += dfs(root.right, curr)
            prefix[curr] -= 1

            return ret

        return dfs(root, 0)
```


深度优先搜索
思路与算法

我们首先想到的解法是穷举所有的可能，我们访问每一个节点 
node
node，检测以 
node
node 为起始节点且向下延深的路径有多少种。我们递归遍历每一个节点的所有可能的路径，然后将这些路径数目加起来即为返回结果。

我们首先定义 
rootSum
(
p
,
val
)
rootSum(p,val) 表示以节点 
p
p 为起点向下且满足路径总和为 
v
a
l
val 的路径数目。我们对二叉树上每个节点 
p
p 求出 
rootSum
(
p
,
targetSum
)
rootSum(p,targetSum)，然后对这些路径数目求和即为返回结果。

我们对节点 
p
p 求 
rootSum
(
p
,
targetSum
)
rootSum(p,targetSum) 时，以当前节点 
p
p 为目标路径的起点递归向下进行搜索。假设当前的节点 
p
p 的值为 
val
val，我们对左子树和右子树进行递归搜索，对节点 
p
p 的左孩子节点 
p
l
p 
l
​
  求出 
rootSum
(
p
l
,
targetSum
−
val
)
rootSum(p 
l
​
 ,targetSum−val)，以及对右孩子节点 
p
r
p 
r
​
  求出 
rootSum
(
p
r
,
targetSum
−
val
)
rootSum(p 
r
​
 ,targetSum−val)。节点 
p
p 的 
rootSum
(
p
,
targetSum
)
rootSum(p,targetSum) 即等于 
rootSum
(
p
l
,
targetSum
−
val
)
rootSum(p 
l
​
 ,targetSum−val) 与 
rootSum
(
p
r
,
targetSum
−
val
)
rootSum(p 
r
​
 ,targetSum−val) 之和，同时我们还需要判断一下当前节点 
p
p 的值是否刚好等于 
targetSum
targetSum。

我们采用递归遍历二叉树的每个节点 
p
p，对节点 
p
p 求 
rootSum
(
p
,
val
)
rootSum(p,val)，然后将每个节点所有求的值进行相加求和返回。

代码
```py

class Solution:
    def pathSum(self, root: TreeNode, targetSum: int) -> int:
        def rootSum(root, targetSum):
            if root is None:
                return 0

            ret = 0
            if root.val == targetSum:
                ret += 1

            ret += rootSum(root.left, targetSum - root.val)
            ret += rootSum(root.right, targetSum - root.val)
            return ret
        
        if root is None:
            return 0
            
        ret = rootSum(root, targetSum)
        ret += self.pathSum(root.left, targetSum)
        ret += self.pathSum(root.right, targetSum)
        return ret
```