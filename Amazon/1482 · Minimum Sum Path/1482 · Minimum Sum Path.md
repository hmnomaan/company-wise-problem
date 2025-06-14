### 1482 · Minimum Sum Path
Algorithms
Medium
Accepted Rate
74%


### Description
Given a BST, find the path with the minimum sum from root to leaves.

## (i)
For the i-th node in array, its left son is 2 * i + 1 in array, its right son is 2 * i + 2 in array, ‘#’ means is null.




## Example
```py
Input:[5,2,6,#,3,#,8]
Output:10
Explanation:
5+2+3=10

```
```py
Input:[1,4,5,3,#,#,6]
Output:8
Explanation:
1+4+3=8

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
    @param root: the root
    @return: minimum sum
    """
    def minimum_sum(self, root: TreeNode) -> int:
        # Write your code here

```

### Tags
Depth First Search/DFS
Divide and Conquer
## Company
Amazon

### Related Problems






### best answer
```py
import functools
import json

from typing import (
    List,
)

number = 0
txt = "\n"


def hook(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        global number, txt
        number += 1
        result = func(*args, **kwargs)
        txt += f"{func.__name__}->{number}->{args[1:]}->{result}\n"
        assert number < 18, txt
        return result
    return wrapper

"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""
class Node:
    #def __init__(self,x):
    def dfs(self,root) :
        if root.left==None and root.right==None :
               return root.val
        if root.left!=None and root.right!=None :
            return root.val+min(self.dfs(root.left),self.dfs(root.right))
        elif root.left!=None :
            return root.val+self.dfs(root.left)
        elif root.right!=None :
            return root.val+self.dfs(root.right)
class Solution:
    """
    @param root: the root
    @return: minimum sum
    """
    def minimumSum(self, root):
        # Write your code here
        ans=Node()
        return ans.dfs(root)
```
```py
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
    @param root: the root
    @return: minimum sum
    """
    def minimum_sum(self, root: TreeNode) -> int:
        # Write your code here
        
        def recur_sum(node):
            if node and not node.left and not node.right:
                return node.val

            left = float("inf")
            right = float("inf")

            if node.left:
                left = recur_sum(node.left)
            
            if node.right:
                right = recur_sum(node.right)

            return node.val + min(left, right)

        return recur_sum(root)
```
```py
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
    @param root: the root
    @return: minimum sum
    """
    def minimum_sum(self, root: TreeNode) -> int:
        return self.dfs(root)

    def dfs(self, root):
        if not root:
            return 0
        L = self.dfs(root.left)
        R = self.dfs(root.right)
        if L and R:
            return root.val + min(L, R)
        if L:
            return root.val + L 
        return root.val + R
        

```



### Official answer from lintcode
考点：

dfs
二叉树遍历
题解：
BST数据给出，故只需遍历求和比较即可，return root.val+min(self.dfs(root.left),self.dfs(root.right)),此处按照左右儿子节点是否存在判断分类。
```py
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""
class Node:
    #def __init__(self,x):
    def dfs(self,root) :
        if root.left==None and root.right==None :
               return root.val
        if root.left!=None and root.right!=None :
            return root.val+min(self.dfs(root.left),self.dfs(root.right))
        elif root.left!=None :
            return root.val+self.dfs(root.left)
        elif root.right!=None :
            return root.val+self.dfs(root.right)
class Solution:
    """
    @param root: the root
    @return: minimum sum
    """
    def minimumSum(self, root):
        # Write your code here
        ans=Node()
        return ans.dfs(root)
```
//2
dfs解决掉
```py
def minimum_sum(self, root: TreeNode) -> int:
    self.ans = float('inf')
    def dfs(node, x):
        if node:
            x += node.val
            if not node.left and not node.right:
                self.ans = min(self.ans, x)
                return
            dfs(node.left, x)
            dfs(node.right, x)
    dfs(root, 0)
    return self.ans
```