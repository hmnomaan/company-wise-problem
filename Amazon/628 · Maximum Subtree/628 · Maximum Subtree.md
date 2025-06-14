### 628 · Maximum Subtree

Algorithms
Easy
Accepted Rate
55%

### Description

Description
Given a binary tree, find the subtree with maximum sum. Return the root of the subtree.

## (i)

LintCode will print the node you return as the optimal subtree.
It's guaranteed that there is only one subtree with maximum sum and the given binary tree is not an empty tree.

## Example

1

```python
Input:
{1,-5,2,0,3,-4,-5}
Output:3
Explanation:
The tree is look like this:
     1
   /   \
 -5     2
 / \   /  \
0   3 -4  -5
The sum of subtree 3 (only one node) is the maximum. So we return 3.

```

```python
Input:
{1}
Output:1
Explanation:
The tree is look like this:
   1
There is one and only one subtree in the tree. So we return 1.

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
    @param root: the root of binary tree
    @return: the maximum weight node
    """
    def find_subtree(self, root: TreeNode) -> TreeNode:
        # write your code here

```

### Tags

Binary Tree
Depth First Search/DFS
Divide and Conquer

## Company

Amazon

### Related Problems

596
Minimum Subtree
Easy

597
Subtree with Maximum Average
Easy

632
Binary Tree Maximum Node
Easy
Recommend Courses

Twitter 后端系统 - Python 项目实战
从0项目经验到深度后端项目操盘，FB架构师万行代码还原真实开发环境，14周简历镀金
35/162

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
    @return: the maximum weight node
    """
    def find_subtree(self, root: TreeNode) -> TreeNode:
        # write your code here
        if not root:
            return None
        node_sum, max_sum, max_leaf = self.get_path(root)
        print('out', node_sum, max_sum, max_leaf)
        return max_leaf
        
        
    def get_path(self, node):
        if not node:
            return 0, 0, None

        if not node.left and not node.right:
            return node.val, node.val, node

        left_sum, left_max, left_leaf = 0, -float('inf'), None
        right_sum, right_max, right_leaf = 0, -float('inf'), None
        if node.left:
            left_sum, left_max, left_leaf = self.get_path(node.left)
        if node.right:
            right_sum, right_max, right_leaf = self.get_path(node.right)
     
        node_sum = left_sum + right_sum + node.val
        max_sum = max(left_max, right_max, node_sum)
        if max_sum == left_max:
            return node_sum, max_sum, left_leaf
        if max_sum == right_max:
            return node_sum, max_sum, right_leaf
        return node_sum, max_sum, node
        
            
    
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
    @param root: the root of binary tree
    @return: the maximum weight node
    """

    def find_subtree(self, root: TreeNode) -> TreeNode:
        # write your code here
        self.max_sum = -float('inf')
        self.max_root = None

        def helper(node):
            if not node:
                return 0
            
            left_sum = helper(node.left)
            right_sum = helper(node.right)

            total_sum = node.val + left_sum + right_sum

            if total_sum > self.max_sum:
                self.max_sum = total_sum
                self.max_root = node
            
            return total_sum
        
        helper(root)
        return self.max_root


        return self.helper(root, -99999)
```
### Official answer from lintcode
Take each point as the root node root (that is, each subtree), find the node x of the left subtree and the node y of the right subtree. If root.val + x.val + y.val > the currently known maximum value, update the answer.
```py
class Solution:
    # @param {TreeNode} root the root of binary tree
    # @return {int} the maximum weight node
    import sys
    maximum_weight = 0
    result = None

    def findSubtree(self, root):
        # Write your code here
        self.helper(root)

        return self.result

    def helper(self, root):
        if root is None:
            return 0

        left_weight = self.helper(root.left)
        right_weight = self.helper(root.right)
        
        if left_weight + right_weight + root.val >= self.maximum_weight or self.result is None:
            self.maximum_weight = left_weight + right_weight + root.val
            self.result = root

        return left_weight + right_weight + root.val
```
