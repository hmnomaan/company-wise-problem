### 629 · Minimum Spanning Tree
Algorithms
Hard
Accepted Rate
43%



### Description

Given a list of Connections, which is the Connection class (the city name at both ends of the edge and a cost between them), find edges that can connect all the cities and spend the least amount.
Return the connection method if all cities can be connected, otherwise return empty list.

## (i)
Return the connections sorted by the cost, or sorted city1 name if their cost is same, or sorted city2 if their city1 name is also same

## Example
1
```python
Input:
["Acity","Bcity",1]
["Acity","Ccity",2]
["Bcity","Ccity",3]
Output:
["Acity","Bcity",1]
["Acity","Ccity",2]

```
2
```python
Input:
["Acity","Bcity",2]
["Bcity","Dcity",5]
["Acity","Dcity",4]
["Ccity","Ecity",1]
Output:
[]

Explanation:
No way

```
### SOLVE this:

```python
'''
Definition for a Connection
class Connection:

    def __init__(self, city1, city2, cost):
        self.city1, self.city2, self.cost = city1, city2, cost
'''
class Solution:
    # @param {Connection[]} connections given a list of connections
    # include two cities and cost
    # @return {Connection[]} a list of connections from results
    def lowestCost(self, connections):
        # Write your code here

```

### Tags
Graph
Greedy
Minimum Spanning Tree/MST
Union Find
## Company
Amazon

### Related Problems

591
Connecting Graph III
Medium

589
Connecting Graph
Medium

590
Connecting Graph II
Medium

434
Number of Islands II
Medium

1765
Spatial connection
Medium





### best answer
```py
'''
Definition for a Connection
class Connection:

    def __init__(self, city1, city2, cost):
        self.city1, self.city2, self.cost = city1, city2, cost
'''

class UnionFind:
    def __init__(self):
        self.father = {}
        self.size = 0
    
    def add(self, u):
        if u not in self.father:
            self.father[u] = u
            self.size += 1
    
    def union(self, a, b):
        root_a, root_b = self.find(a), self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.size -= 1

    def is_connected(self, a, b):
        root_a, root_b = self.find(a), self.find(b)
        return root_a == root_b
        
    def find(self, a):
        path = []
        while self.father[a] != a:
            path.append(a)
            a = self.father[a]
        for u in path:
            self.father[u] = a
        return a

class Solution:
    # @param {Connection[]} connections given a list of connections
    # include two cities and cost
    # @return {Connection[]} a list of connections from results
    def lowestCost(self, connections):
        # Write your code here
        union = UnionFind()
        # for connection in connections:
        #     city1, city2, cost = connection.city1, connection.city2, connection.cost
        #     union.add(city1)
        #     union.add(city2)
        connections.sort(key=lambda x: (x.cost, x.city1, x.city2))
        ans = []
        for connection in connections:
            city1, city2, cost = connection.city1, connection.city2, connection.cost
            union.add(city1)
            union.add(city2)
            if union.is_connected(city1, city2):
                continue
            union.union(city1, city2)
            ans.append(connection)
            
        if union.size == 1:
            return ans
        return []
```


### Official answer from lintcode
Use map to store automatic sorting, then use union to find the set, the roots of connected points should be the same.
```py
'''
Definition for a Connection
class Connection:

    def __init__(self, city1, city2, cost):
        self.city1, self.city2, self.cost = city1, city2, cost
'''
import functools

def comp(a, b):
    if a.cost != b.cost:
        return a.cost - b.cost
    
    if a.city1 != b.city1:
        if a.city1 < b.city1:
            return -1
        else:
            return 1

    if a.city2 == b.city2:
        return 0
    elif a.city2 < b.city2:
        return -1
    else:
        return 1

class Solution:
    # @param {Connection[]} connections given a list of connections include two cities and cost
    # @return {Connection[]} a list of connections from results
    def lowestCost(self, connections):
        # Write your code here
        connections.sort(key=functools.cmp_to_key(comp))
        hash = {}   
        n = 0
        for connection in connections:
            if connection.city1 not in hash:
                n += 1
                hash[connection.city1] = n
            
            if connection.city2 not in hash:
                n += 1
                hash[connection.city2] = n

        father = [0 for _ in range(n + 1)] 

        results = []
        for connection in connections:
            num1 = hash[connection.city1]
            num2 = hash[connection.city2]

            root1 = self.find(num1, father)
            root2 = self.find(num2, father)
            if root1 != root2:
                father[root1] = root2
                results.append(connection)

        if len(results)!= n - 1:
            return []
        return results
    
    def find(self, num, father):
        if father[num] == 0:
            return num
        father[num] = self.find(father[num], father)
        return father[num]
```