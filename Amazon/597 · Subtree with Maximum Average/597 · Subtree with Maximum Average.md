## 597 · Subtree with Maximum Average
Algorithms
Easy
Accepted Rate
36%


## Description
Given a binary tree, find the subtree with maximum average. Return the root of the subtree.

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
    @param root: the root of binary tree
    @return: the root of the maximum average of subtree
    """
    def find_subtree2(self, root: TreeNode) -> TreeNode:
        # write your code here
```


## (i)

``````1 LintCode will print the subtree which root is your return node. It's guaranteed that there is only one subtree with maximum average``````
`````2 A subtree is a tree consists of a node in it and all of this node's descendants. The tree itself could also be considered as a subtree of itself
`````

Example
Example 1

```python
Input：
{1,-5,11,1,2,4,-2}
Output：11
Explanation:
The tree is look like this:
     1
   /   \
 -5     11
 / \   /  \
1   2 4    -2 
The average of subtree of 11 is 4.3333, is the maximun.
```

Example 2

```python

Input：
{1,-5,11}
Output：11
Explanation:
     1
   /   \
 -5     11
The average of subtree of 1,-5,11 is 2.333,-5,11. So the subtree of 11 is the maximun.

```

## Tags
Binary Tree
Depth First Search/DFS
Divide and Conquer

## Company
Amazon

## Related Problems

596
Minimum Subtree
Easy

628
Maximum Subtree
Easy

632
Binary Tree Maximum Node
Easy




### best answer
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
    @param root: the root of binary tree
    @return: the root of the maximum average of subtree
    """
    def find_subtree2(self, root: TreeNode) -> TreeNode:
        # write your code here
        max_node, max_average, root_sum, node_count = self.get_average(root)
        return max_node
    
    def get_average(self, root):
        if not root:
            return None, float('-inf'), 0, 0
        
        left_max_node, left_max_average, left_sum, left_node_count = self.get_average(root.left)
        right_max_node, right_max_average, right_sum, right_node_count = self.get_average(root.right)

        node_count = left_node_count + right_node_count + 1
        curr_sum = left_sum + right_sum + root.val
        curr_average = curr_sum / node_count
        max_average = max(left_max_average, right_max_average, curr_average)

        if max_average == left_max_average:
            return left_max_node, left_max_average, curr_sum, node_count
        if max_average == right_max_average:
            return right_max_node, right_max_average, curr_sum, node_count
        if max_average == curr_average:
            return root, curr_average, curr_sum, node_count

```



### Official answer from lintcode

```py
class Solution:
    # @param {TreeNode} root the root of binary tree
    # @return {TreeNode} the root of the maximum average of subtree
    average, node = 0, None

    def findSubtree2(self, root):
        # Write your code here
        self.helper(root)
        return self.node

    def helper(self, root):
        if root is None:
            return 0, 0

        left_sum, left_size = self.helper(root.left)
        right_sum, right_size = self.helper(root.right)

        sum, size = left_sum + right_sum + root.val, \
                    left_size + right_size + 1

        if self.node is None or sum * 1.0 / size > self.average:
            self.node = root
            self.average = sum * 1.0 / size

        return sum, size
```