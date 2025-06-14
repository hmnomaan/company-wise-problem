### 808 · Movie Network
Algorithms
Medium
Accepted Rate
35%



### Description
Give some rating of movie (number starting from 0) and their relationship, and relationships can be passed (a and b are related, b and c are related, a and c are also considered to be related). Give every movie's relationship list.Given a movie numbered S, find the top K movies with the highest rating in the movies associated with S(When the number of movies which associated with S is less than K, output all the movies .You can output them in any order). Does not include this movie.

(i)
the number of movies is n, and n <= 20000.
We guarantee that the number is 0 ~ n-1.
We guarantee that the numbers of the 2 vertices of an edge both belong to 0 ~ n-1.
We guarantee that the numbers of the edges is m, and m <= 100000.
We guarantee that the rating of each movie is not the same.


## Example
1
```python
Input:  
ratingArray = [10,20,30,40], 
contactRelationship = [[1,3],[0,2],[1],[0]], 
S = 0, K = 2
Output:  [2,3]	
Explanation:
	In contactRelationship, [1,3] is associated with 0,[0,2] is associated with 1,[1] is associated 2,[0] is associated with 3.
	Finally,Movies numbered [1,2,3] are associated with movie 0, and the order which according to their rating from high to low is [3,2,1], so the output [2,3].

```
2
```python
Input:  
ratingArray = [10,20,30,40,50,60,70,80,90], 
contactRelationship = [[1,4,5],[0,2,3],[1,7],[1,6,7],[0],[0],[3],[2,3],[]], 
S = 5, K = 3
Output:  [6,7,4]	
Explanation:
	In contactRelationship,[1,4,5] is associated with 0,[0,2,3] is associated with 1,[1,7] is associated with 2,[1,6,7] is is associated with 3,[0] is associated with 4,[0] is associated with 5,[3] is associated with 6,[2,3] is associated with 7,no moive is associated with 8.
	Finally,Movies numbered [0,1,2,3,4,6,7] are associated with movie 5, and the order which according to their rating from high to low is [7,6,4,3,2,1,0]. Notice that movie 8 is not related to movie 5, so it has the highest rating but does not count towards the answer.	

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param rating: the rating of the movies
    @param g: the realtionship of movies
    @param s: the begin movie
    @param k: top K rating 
    @return: the top k largest rating moive which contact with S
             we will sort your return value in output
    """
    def top_k_movie(self, rating: List[int], g: List[List[int]], s: int, k: int) -> List[int]:
        # Write your code here

```

### Tags
Depth First Search/DFS
Heap
## Company
Amazon

### Related Problems


790
Parser
Medium




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
        assert number < 1, txt
        return result
    return wrapper

import heapq
class Solution:
    """
    @param rating: the rating of the movies
    @param G: the realtionship of movies
    @param S: the begin movie
    @param K: top K rating 
    @return: the top k largest rating moive which contact with S
    """
    def topKMovie(self, rating, G, S, K):
        # Write your code here
        # use queue to solve this 
        queue = []
        heap = []
        visited = set()
        result = []
        
        queue.append(S)
        visited.add(S)
        while len(queue):
            cur = queue.pop(0)
            relation = G[cur]
            for i in relation:
                if i in visited:
                    continue
                if len(heap) < K:
                    heapq.heappush(heap, [rating[i], i])
                else:
                    if rating[i] > heap[0][0]:
                        heapq.heappop(heap)
                        heapq.heappush(heap, [rating[i], i])
                visited.add(i)
                queue.append(i)
                
        for element in heap:
            result.append(element[1])
            
        return result
```
```py
class Solution:
    """
    @param rating: the rating of the movies
    @param G: the realtionship of movies
    @param S: the begin movie
    @param K: top K rating 
    @return: the top k largest rating moive which contact with S
    """
    def topKMovie(self, rating, G, S, K):
        # Write your code here
        from collections import deque
        dq = deque([S])
        import heapq
        hq = list()
        movieSeen = set([S])
        
        while dq:
            movie = dq.popleft()
            if movie != S:
                heapq.heappush(hq, (rating[movie], movie))
            if len(hq) > K:
                heapq.heappop(hq)
            for relatedMovie in G[movie]:
                if not relatedMovie in movieSeen:
                    dq.append(relatedMovie)
                    movieSeen.add(relatedMovie)
        
        res = list()       
        while hq:
            res.append(heapq.heappop(hq)[1])
        return res
```

### Official answer from lintcode
Just start DFS from S and maintain a priority queue of size K.
```py
import Queue
class Solution:
    """
    @param rating: the rating of the movies
    @param G: the realtionship of movies
    @param S: the begin movie
    @param K: top K rating 
    @return: the top k largest rating moive which contact with S
    """
    def __init__(self):
        self.visit = {}
        self.Q = Queue.PriorityQueue() 
    class node :
        def __init__(self, rating, id):
            self.id = id
            self.rating = rating
        def __cmp__(self, other):
            return self.rating > other.rating
    def dfs(self, u, limit, rating, G, S):
        self.visit[u] = 1
        First = self.node(0,0)
        if self.Q.qsize() != 0:
            First = self.Q.get()
            self.Q.put(First)
        if u != S:
            if self.Q.qsize() < limit or rating[u] > First.rating:
                if self.Q.qsize() == limit:
                    self.Q.get()
                self.Q.put(self.node(rating[u],u))
        for i in G[u]:
            if i not in self.visit:
                self.dfs(i, limit, rating, G, S)
        
    def topKMovie(self, rating, G, S, K):
        
        # Write your code here
        ans = []
        self.dfs(S, K, rating, G, S)
        while self.Q.empty() is False:
            ans.append(self.Q.get().id)
        return ans
```