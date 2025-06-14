### 1562 · Number of restaurants
Algorithms
Medium
Accepted Rate
30%


### Description
Give a List of data representing the coordinates[x,y] of each restaurant and the customer is at the origin[0,0]. Find n closest restaurants to the customer, where m is the furthest distance from n restaurants to the customer. If there are more than n restaurants in the list and the distance from the customer is not greater than m, then the first n restaurants will be returned in the order of the elements in the list.
## (i)
1.Coordinates in range [-1000,1000]
2.n>0
3.No same coordinates




## Example
```python
Input: n = 2 , List = [[0,0],[1,1],[2,2]]
Output : [[0,0],[1,1]]
Explanation: The closest 2 restaurants are [0,0] and [1,1]. And only these two restaurants are in sqrt(2) meters.

```
```python
Input: n = 3,List = [[0,1],[1,2],[2,1],[1,0]]
Output:[[0,1],[1,2],[2,1]]
Explanation: The closest 3 restaurants are [0,1],[1,2] and [2,1]. And only these three restaurants are in sqrt(5) meters. 

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param restaurant: 
    @param n: 
    @return: 
    """
    def nearest_restaurant(self, restaurant: List[List[int]], n: int) -> List[List[int]]:
        # Write your code here

```

### Tags
Sort
## Company
Amazon

### Related Problems






### best answer
```py
class Solution:
    """
    @param restaurant: 
    @param n: 
    @return: nothing
    """
    def nearestRestaurant(self, restaurant, n):
        # Write your code here
        if len(restaurant) < n:
            return []
        sorted_res = []
        for i in range(len(restaurant)):
            sorted_res.append((restaurant[i], i))
        sorted_res = sorted(sorted_res, key=lambda x: x[0][0]**2+x[0][1]**2)[:n]
        
        sorted_res = sorted(sorted_res, key=lambda x: x[1])    
        
        return [sorted_res[x][0] for x in range(n)]
```
//
2
```py
class Solution:
    """
    @param restaurant: 
    @param n: 
    @return: nothing
    """

    def distance(self,x,y):
        return x**2 + y**2 
    def nearestRestaurant(self, restaurant, n):
        if len(restaurant) == 0 or len(restaurant) < n:
            return []
        import heapq 
        order = []
        result = []
        res = []
        for i , (x,y) in enumerate(restaurant):
           heapq.heappush(order,(self.distance(x,y),i,[x,y]))
        # 则按列表内元素顺序返回先出现的 n 家餐厅， 注意不是远近顺序
        for i in range(n):
            heapq.heappush(result,(heapq.heappop(order)[1:]))
        for i in range(n):
            res.append(heapq.heappop(result)[1])
 
    
        return res
```
```py
class Solution:
    """
    @param restaurant: 
    @param n: 
    @return: nothing
    """
    def nearestRestaurant(self, restaurant, n):
        # Write your code here
        result = []
        if(restaurant == None or len(restaurant) == 0 or n > len(restaurant)):
            return result
        L = len(restaurant)
        distance = []
        count = 0
        for coordinates in restaurant:
            dis = int(coordinates[0])**2 + int(coordinates[1])**2
            distance.append(dis)
        distance.sort()
        for coordinates in restaurant:
            dis = int(coordinates[0])**2 + int(coordinates[1])**2
            if(dis <= distance[n - 1]):
                result.append(coordinates)
                count +=1
            if(count == n):
                break
        return result
```


### Official answer from lintcode

```py
class Solution:
    """
    @param restaurant: 
    @param n: 
    @return: nothing
    """
    def nearestRestaurant(self, restaurant, n):
        # Write your code here
        result = []
        if(restaurant == None or len(restaurant) == 0 or n > len(restaurant)):
            return result
        L = len(restaurant)
        distance = []
        count = 0
        for coordinates in restaurant:
            dis = int(coordinates[0])**2 + int(coordinates[1])**2
            distance.append(dis)
        distance.sort()
        for coordinates in restaurant:
            dis = int(coordinates[0])**2 + int(coordinates[1])**2
            if(dis <= distance[n - 1]):
                result.append(coordinates)
                count +=1
            if(count == n):
                break
        return result
```
//
2
find the max distance first then go over the list to select n restaurants
```py
class Solution:
    """
    @param restaurant: 
    @param n: 
    @return: nothing
    """
    def nearestRestaurant(self, restaurant, n):
        # don't agree with this case
        if len(restaurant) < n:
            return []
            
        if len(restaurant) == n:
            return restaurant
            
        distance = lambda c: c[0] ** 2 + c[1] ** 2
        max_dist = sorted([(distance(c), i) for i, c in enumerate(restaurant)])[n - 1][0]
        
        res = [c for i, c in enumerate(restaurant) if distance(c) <= max_dist][:n]
        
        return res
```