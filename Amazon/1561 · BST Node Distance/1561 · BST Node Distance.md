### 1561 · BST Node Distance

Algorithms
Medium
Accepted Rate
42%

### Description

Given an integer array (unordered) and two node values, construct a BST from it(you need to insert nodes one-by-one with the given order to get the BST) and find the distance between two given nodes.

## (i)

If two nodes do not appear in the BST, return -1
We guarantee that there are no duplicate nodes in BST
The node distance means the number of edges between two nodes

## Example

```python
Input:
numbers = {2,1,3}
node1 = 1
node2 = 3
Output:
2
Explaination:
The tree is look like this.
  2
 / \
1  3

```

```python
Input:
numbers = {2,1}
node1 = 1
node2 = 3
Output: -1

```

### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param numbers: the given list
    @param node1: the given node1
    @param node2: the given node2
    @return: the distance between two nodes
    """
    def bst_distance(self, numbers: List[int], node1: int, node2: int) -> int:
        # Write your code here

```

### Tags
Binary Tree
Binary Search Tree
Depth First Search/DFS
## Company

Amazon

### Related Problems

### best answer

```py
from typing import (
    List,
)

def find_path(nums, target):
    path = []
    lo = -float("inf")
    hi = float("inf")
    for x in nums:
        if lo < x < hi:
            path.append(x)
            if x < target:
                lo = x
            elif x > target:
                hi = x
            else:
                return path
    return []

class Solution:
    """
    @param numbers: the given list
    @param node1: the given node1
    @param node2: the given node2
    @return: the distance between two nodes
    """
    def bst_distance(self, nums: List[int], node1: int, node2: int) -> int:
        # Write your code here

        path1 = find_path(nums, node1)
        if not path1:
            return -1
        path2 = find_path(nums, node2)
        if not path2:
            return -1
        
        i = 0
        while i < len(path1) and i < len(path2) and path1[i] == path2[i]:
            i += 1
        
        return len(path1) + len(path2) - 2 * i
```
```py
class Solution:
    """
    @param numbers: the given list
    @param node1: the given node1
    @param node2: the given node2
    @return: the distance between two nodes
    """
    def bstDistance(self, numbers, node1, node2):
        # Write your code here
        path1 = self.get_path(numbers, node1)
        path2 = self.get_path(numbers, node2)

        if len(path1) == 0 or len(path2) == 0:
            return -1 
        
        index = 0 
        while index < len(path1) and index < len(path2):
            if path1[index] != path2[index]:
                break 
            index += 1 
        
        return len(path1) + len(path2) - 2 * index 
    
    def get_path(self, numbers, target):
        left, right = -sys.maxsize, sys.maxsize 
        result = []
        for number in numbers:
            if left < number < right:
                result.append(number)
                if number == target:
                    return result 
                elif number < target:
                    left = number 
                else:
                    right = number 
        
        return []
```
```py
from typing import (
    List,
)

class Solution:
    """
    @param numbers: the given list
    @param node1: the given node1
    @param node2: the given node2
    @return: the distance between two nodes
    """
    def bst_distance(self, numbers: List[int], node1: int, node2: int) -> int:
        
        def reverse(numbers, target):
            left, right = float("-inf"), float("inf")
            result = []

            for number in numbers:
                if left < number < right:
                    result.append(number)

                    if number == target:
                        return result
                    elif number < target:
                        left = number
                    else:
                        right = number
            
            return []
        
        path1 = reverse(numbers, node1)
        path2 = reverse(numbers, node2)
        length1, length2 = len(path1), len(path2)

        if length1 == 0 or length2 == 0:
            return -1

        index = 0

        while index < length1 and index < length2:
            if path1[index] != path2[index]:
                break
            
            index += 1
        
        return length1 + length2 - 2 * index
```
### Official answer from lintcode

```py
class Solution:
    """
    @param numbers: the given list
    @param node1: the given node1
    @param node2: the given node2
    @return: the distance between two nodes
    """

    def insert(self, root, node):
        if root is None:
            return TreeNode(node)
        
        if root.val > node:
            root.left = self.insert(root.left, node)
        elif root.val < node:
            root.right = self.insert(root.right, node)
        
        return root

    
    def buildTree(self, numbers):
        root = TreeNode(numbers[0])
        length = len(numbers)
        for i in range(1, length):
            self.insert(root, numbers[i])
        
        return root
    
    
    def findDis(self, root, node):
        dis = 0
        while root.val != node:
            dis += 1
            if root.val > node:
                root = root.left
            else:
                root = root.right
        return dis
    
    def check(self, numbers, node1, node2):
        Set = set()
        for i in range(0, len(numbers)):
            Set.add(numbers[i])

        if node1 in Set and node2 in Set:
            return True
        return False
     
    def bstDistance(self, numbers, node1, node2):
        # Write your code here
        if numbers is None or len(numbers) < 2:
            return -1
        
        if not self.check(numbers, node1, node2):
            return -1
        
        root = self.buildTree(numbers)
        while node1 > root.val and node2 > root.val or node1 < root.val and node2 < root.val:
            if node1 > root.val and node2 > root.val:
                root = root.right
            else:
                root = root.left
        return self.findDis(root, node1) + self.findDis(root, node2)
```
