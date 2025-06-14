### 806 · Buy Fruits
Algorithms
Medium
Accepted Rate
37%



### Description
Xiao Ming is going to help companies buy fruit. Give a codeList, which is loaded with the fruit he bought. Give a shoppingCart, which is loaded with target fruit. We need to check if the order in the codeList matches the order in the shoppingCart. Note that only the sum of the items in all linked lists in the codeList add up to less than or equal to the sum of items in the shoppingcart may return 1. In addition, the item in codeList may be "anything", which can match with any fruit.

## i
The number of fruits in codeList and the number of fruits in shppingCart are both less than 2000.




## Example
```python
Input:  codeList = [["apple", "apple"],["orange", "banana", "orange"]], shoppingCart = ["orange", "apple", "apple", "orange", "banana", "orange"]
Output:  1	
Explanation: Because the order in the codeList matches the fruit in the shoppingCart except for the first orange.

```
```python
Input:  codeList = [["orange", "banana", "orange"],["apple", "apple"]], shoppingCart = ["orange", "apple", "apple", "orange", "banana", "orange"]
Output:  0	
Explanation: Because the order in the codeList doesn't match the shoppingCart.

```

```py
Input:  codeList = [["apple", "apple"],["orange", "anything", "orange"]], shoppingCart = ["orange", "apple", "apple", "orange", "mango", "orange"]
Output:  1	
Explanation: anything matches mango, so codeList can match the fruit of shoppingCart.
```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param code_list: The codeList
    @param shopping_cart: The shoppingCart
    @return: The answer
    """
    def buy_fruits(self, code_list: List[List[str]], shopping_cart: List[str]) -> int:
        # Write your code here

```

### Tags
Tags
Enumerate
String
## Company
Amazon

### Related Problems






### best answer
```py
class Solution:
    """
    @param codeList: The codeList
    @param shoppingCart: The shoppingCart
    @return: The answer
    """
    def buyFruits(self, codeList, shoppingCart):
        A = []
        for items in codeList:
            for item in items:
                A.append(item)
        B = shoppingCart
        
        i = j = 0
        while j < len(B):
            if A[i] == B[j] or A[i] == "anything":
                i += 1
            else:
                j -= i 
                i = 0
            j += 1
            if i == len(A):
                return 1 
        return 0
```


### Official answer from lintcode
First, determine the size of codeList and shoppingCart, and then check them in two layers of for loops.
```py
class Solution:
    """
    @param codeList: The codeList
    @param shoppingCart: The shoppingCart
    @return: The answer
    """
    def buyFruits(self, codeList, shoppingCart):
        # Write your code here
        sumCodeList = 0
        for itemList in codeList:
            sumCodeList += len(itemList)
        sumShoppingCart = len(shoppingCart)
        if sumCodeList > sumShoppingCart:
            return 0
        for i in range(sumShoppingCart - sumCodeList + 1):
            idx = 0
            for itemList in codeList:
                for j in itemList:
                    if j == shoppingCart[i + idx] or j == 'anything':
                        idx += 1
                    else:
                        idx = -1
                        break
                if idx == -1:
                    break
            if idx == sumCodeList:
                return 1
        return 0
```