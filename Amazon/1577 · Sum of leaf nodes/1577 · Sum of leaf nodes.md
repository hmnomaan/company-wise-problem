### 1577 · Sum of leaf nodes
Algorithms
Medium
Accepted Rate
74%


### Description
Given a binary tree, find the sum of all leaf nodes.




## Example
```python
Input:
{1,2,3,4,5}
Output : 12

Explanation：
      1
     / \
   2   3
  / \     
4   5    
Leaf nodes are nodes without children. 4+5+3 = 12

```
```python
Input：
{12,3,7,4,5,#,#,2}
Output：14

Explanation：
      12
      / \
    3   7
   / \     
 4   5    
/
2
2+5+7 = 14


```
## Challenge
Of course, you can use depth or breadth first traversal, but can you solve this problem with a space complexity of O(1) ?

Hide Hint
You can try to use the Morris algorithm to solve this problem





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
    @return: the sum of leafnode
    """
    def sum_leaf_node(self, root: TreeNode) -> int:
        # Write your code here

```

### Tags
Tags
Binary Tree
Divide and Conquer

## Company
Google
Amazon

### Related Problems






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
    @param root: 
    @return: the sum of leafnode
    """
    def sum_leaf_node(self, root: TreeNode) -> int:
        # Write your code here
        res = 0
        def dfs(root=root):
            nonlocal res
            if not root:return
            if root.left==root.right:
                res += root.val
            dfs(root.left)
            dfs(root.right)
        dfs()
        return res
```
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
    @return: the sum of leafnode
    """
    def sumLeafNode(self, root):
        # Write your code here
        if not root:
            return 0
        if not root.left and not root.right:
            return root.val
        left = self.sumLeafNode(root.left)
        right = self.sumLeafNode(root.right)
        return left + right
```
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
    @return: the sum of leafnode
    """
    def __init__(self):
        self.all_sum = 0

    def search(self,node):

        if node.left == None and node.right == None:
            self.all_sum += node.val

        elif node.left == None:
            self.search(node.right)

        elif node.right == None:
            self.search(node.left)
        else:
            self.search(node.left)
            self.search(node.right)
    def sumLeafNode(self, root):
        # Write your code here
        
        self.search(root)

        return self.all_sum
```
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
    @return: the sum of leafnode
    """
    sum = 0
    def sumLeafNode(self, root):
        # Write your code here
        p = []
        self.dfs(root, p)
        return sum(p)

        
    def dfs(self, root, p):
        if root is None:
            return
        if root.left is None and root.right is None:
            p.append(root.val)
        self.dfs(root.left, p)
        self.dfs(root.right, p)
```


### Official answer from lintcode
Morris算法使用二叉树中的叶节点的right指针来保存后面将要访问的节点的信息，当这个right指针使用完成之后，再将它置为NULL，但是在访问过程中有些节点会访问两次，所以它的空间复杂度为O(1),时间复杂度为O（n）
中序遍历的顺序是左-中-右，即先访问左子树，再访问根节点，最后访问右子树，
对于某个节点N，如果其左子树为空，那么就说明没有左子树，可以将这种情况视为左子树已经访问完毕，
那么这个时候就访问根节点，再将当前节点指针指向根节点的右子树的根节点，进而访问右子树。
如果根节点的的左子树不为空，那么就找到遍历左子树时访问的最后一个节点M(节点M的right指针一定为NULL)，
将这个节点的right指针指向根节点，这样在访问完了根节点的左子树后，就可以根据这个right指针，来访问下面将要访问的节点。
```py
class Solution:
    def sumLeafNode(TreeNode root) :
        int sum = 0;
        
        if root == null:
            return sum;

        TreeNode cur = root;
        while cur != null:
            if cur.left == null and cur.right == null:
                sum += cur.val;
            if cur.left == null:
                cur = cur.right;
            else:
                TreeNode temp = cur.left;
                while temp.right != null and temp.right != cur:
                    temp = temp.right;
                if temp.right == null and temp.left == null: 
                    sum += temp.val;
                if temp.right == null:
                    temp.right = cur;
                    cur = cur.left;
                else:            
                    temp.right = null;
                    cur = cur.right;
    	return sum;
```
//
2
Morris inorder traversal, 利用二叉树中叶节点的right指针来保存接下来要访问的节点，这个right指针使用完成后再重置为None。
不使用递归或栈，空间复杂度O(1)。
```py
# Morris inorder
class Solution:
    """
    @param root: 
    @return: the sum of leafnode
    """
    def sumLeafNode(self, root):
        res = 0
        
        p = root
        while p:
            if p.left is None:
                if p.right is None:  # p is a leaf node
                    res += p.val
                p = p.right
            else:
                tmp = p.left
                while tmp.right is not None and tmp.right != p:
                    tmp = tmp.right
                if tmp.right is None:
                    if tmp.left is None:  # tmp is a leaf node
                        res += tmp.val
                    tmp.right = p
                    p = p.left
                else:
                    tmp.right = None
                    p = p.right
        
        return res
```