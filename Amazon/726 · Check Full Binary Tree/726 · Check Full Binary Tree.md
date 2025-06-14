### 726 · Check Full Binary Tree
Algorithms
Medium
Accepted Rate
67%
 


### Description

A full binary tree is defined as a binary tree in which all nodes have either zero or two child nodes. Conversely, there is no node in a full binary tree, which has one child node. More information about full binary trees can be found here[https://baike.baidu.com/item/%E6%BB%A1%E4%BA%8C%E5%8F%89%E6%A0%91].

```py
Full Binary Tree
      1
     / \
    2   3
   / \
  4   5

Not a Full Binary Tree
      1
     / \
    2   3
   / 
  4   
```



## Example
1
```python
Input: {1,2,3}
Output: true   
Explanation:
      1
     / \
    2   3
It is a full binary tree.

```
2
```python
Input: {1,2,3,4}
Output: false  
Explanation:
      1
     / \
    2   3
   / 
  4   
It is not a full binary tree

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
    @param root: the given tree
    @return: Whether it is a full tree
    """
    def is_full_tree(self, root: TreeNode) -> bool:
        # write your code here

```

### Tags
Binary Tree
## Company
Amazon

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
    @param root: the given tree
    @return: Whether it is a full tree
    """
    def isFullTree(self, root):
        if not root:
            return True
            
        if not root.left and not root.right:
            return True
            
        if root.left and root.right:
            return self.isFullTree(root.left) and self.isFullTree(root.right)
        
        return False
```


### Official answer from lintcode

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
    @param root: the given tree
    @return: Whether it is a full tree
    """
    def isFullTree(self, root):
        # write your code here
        if (root == None) :
            return True
        if (root.left == None and root.right == None):
            return True
        if (root.left != None and root.right != None):
            return (Solution.isFullTree(self, root.left) and Solution.isFullTree(self, root.right))
        return False
```