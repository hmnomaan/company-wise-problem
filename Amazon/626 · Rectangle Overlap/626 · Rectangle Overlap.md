### 626 · Rectangle Overlap
Algorithms
Easy
Accepted Rate
45%



### Description
Description
Given two rectangles, find if the given two rectangles overlap or not.

## (i)

l1: Top Left coordinate of first rectangle.
r1: Bottom Right coordinate of first rectangle.
l2: Top Left coordinate of second rectangle.
r2: Bottom Right coordinate of second rectangle.

l1 != r1 and l2 != r2



## Example
Example 1:
```python
Input : l1 = [0, 8], r1 = [8, 0], l2 = [6, 6], r2 = [10, 0]
Output : true

```
Example 2:

```python
Input : l1 = [0, 8], r1 = [8, 0], l2 = [9, 6], r2 = [10, 0]
Output : false

```
### SOLVE this:

```python
from lintcode import (
    Point,
)

"""
Definition for a point:
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y
"""

class Solution:
    """
    @param l1: top-left coordinate of first rectangle
    @param r1: bottom-right coordinate of first rectangle
    @param l2: top-left coordinate of second rectangle
    @param r2: bottom-right coordinate of second rectangle
    @return: true if they are overlap or false
    """
    def do_overlap(self, l1: Point, r1: Point, l2: Point, r2: Point) -> bool:
        # write your code here

```

### Tags
Computational Geometry
Mathmatics
## Company
Amazon

### Related Problems






### best answer
```py
from lintcode import (
    Point,
)

"""
Definition for a point:
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y
"""

class Solution:
    """
    @param l1: top-left coordinate of first rectangle
    @param r1: bottom-right coordinate of first rectangle
    @param l2: top-left coordinate of second rectangle
    @param r2: bottom-right coordinate of second rectangle
    @return: true if they are overlap or false
    """
    def do_overlap(self, l1: Point, r1: Point, l2: Point, r2: Point) -> bool:
        # write your code here
        if l1.x > r2.x or l2.x > r1.x:
            return False
        if l1.y < r2.y or l2.y < r1.y:
            return False
        
        return True
```


### Official answer from lintcode
Just determine the boundary 1
```py
# Definition for a point.
# class Point:
#     def __init__(self, a=0, b=0):
#         self.x = a
#         self.y = b

class Solution:
    # @param {Point} l1 top-left coordinate of first rectangle
    # @param {Point} r1 bottom-right coordinate of first rectangle
    # @param {Point} l2 top-left coordinate of second rectangle
    # @param {Point} r2 bottom-right coordinate of second rectangle
    # @return {boolean} true if they are overlap or false
    def doOverlap(self, l1, r1, l2, r2):
        # Write your code here
        if l1.x > r2.x or l2.x > r1.x:
            return False

        if l1.y < r2.y or l2.y < r1.y:
            return False
        
        return True
```