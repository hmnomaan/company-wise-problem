### 805 · Maximum Association Set
Algorithms
Medium
Accepted Rate
57%



### Description
Amazon sells books, every book has books which are strongly associated with it. Given ListA and ListB,indicates that ListA [i] is associated with ListB [i] which represents the book and associated books. Output the largest set associated with each other(output in any sort). You can assume that there is only one of the largest set.

## i 
The number of books does not exceed 5000.




## Example
```python
Example 1:
	Input:  ListA = ["abc","abc","abc"], ListB = ["bcd","acd","def"]
	Output:  ["abc","acd","bcd","def"]
	Explanation:
	abc is associated with bcd, acd, dfe, so the largest set is the set of all books
	
Example 2:
	Input:  ListA = ["a","b","d","e","f"], ListB = ["b","c","e","g","g"]
	Output:  ["d","e","f","g"]
	Explanation:
	The current set are [a, b, c] and [d, e, g, f], then the largest set is [d, e, g, f]

```
```python


```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param list_a: The relation between ListB's books
    @param list_b: The relation between ListA's books
    @return: The answer
             we will sort your return value in output
    """
    def maximum_association_set(self, list_a: List[str], list_b: List[str]) -> List[str]:
        # Write your code here

```

### Tags
Union Find
## Company
Amazon

### Related Problems






### best answer
```py
import collections
class Solution:
    """
    @param ListA: The relation between ListB's books
    @param ListB: The relation between ListA's books
    @return: The answer
    """
    def maximumAssociationSet(self, listA, listB):
        # Write your code hered
        graph = collections.defaultdict(list)
        for i in range(len(listA)):
            graph[listA[i]].append(listB[i])
            graph[listB[i]].append(listA[i])
            
        ans = []
        visited = set()
        for book in listA:
            if book not in visited:
                visited.add(book)
                associate = self.bfs(graph, book, visited)
            if len(ans) < len(associate):
                ans = associate
        return ans 
        
    def bfs(self, graph, book, visited):
        queue = collections.deque([book])
        asso = []
        while queue:
            cur = queue.popleft()
            asso.append(cur)
            for nxt in graph[cur]:
                if nxt not in visited:
                    queue.append(nxt)
                    visited.add(nxt)
        return asso
```


### Official answer from lintcode
Algorithm Union-find Algorithm analysis The question gives two lists of book names. Books in the same position in the two lists represent their mutual association. The question requires finding the largest set of books that are mutually associated. The essence of this question is actually a problem of merging and querying disjoint sets. For this kind of problem, ordinary data structures cannot take into account both time complexity and space complexity. In the face of this kind of problem, we can choose the data structure of union-find. Its search and merge functions can solve this problem well. Algorithm steps 1. Data preprocessing: traverse the two lists and use hash to associate each book name with a unique integer. 2. Initialize the union-find array: 𝑓 [ 𝑖 ] = 𝑖 f[i]=i, that is, each book is associated with itself. 3. Union-find operation: For books in the same position in the two lists, call 𝑓 𝑖 𝑛 𝑑 find function and then update the union-find array. 4. Union-find set search operation: count the most frequent numbers in the union-find set, i.e. the largest associated set. 5. Reconvert the numbers to book names, generate a list of book names and output it. Complexity analysis Time complexity: approximately 𝑂 ( 𝑛 ) O(n),  𝑛 n is the number of book names The time complexity of data preprocessing and the final reconversion to string is 𝑂 ( 𝑛 ) O(n), and the time complexity of the union-find set is 𝑂 ( 𝑛 ) O( n⋅Alpha(n)) (Alpha is an inverse function of the Ackerman function) Space complexity: 𝑂 ( 𝑛 ) O(n),  𝑛 n is the number of book names It is necessary to convert strings and numbers into two ℎ 𝑎 𝑠 ℎ 𝑚 𝑎 𝑝 hashmap dictionaries and a union-find array. The length of each is the number of book names.
```py

class Solution:

    # 并查集 find 函数

    def find(self, x, f):

        if f[x] != x:

            f[x] = self.find(f[x], f)

        return f[x]

    def maximumAssociationSet(self, ListA, ListB):

        # digit 记录书籍信息，书籍名称->数字编号

        digit = {}

        # name 记录数字编号->书籍名称

        name = {}

        # 书籍总个数

        n = 0

        # 数据预处理，书籍对应数字编号

        for i in range(0, len(ListA)):

            if ListA[i] not in digit:

                digit[ListA[i]] = n

                name[n] = ListA[i]

                n += 1

            if ListB[i] not in digit:

                digit[ListB[i]] = n

                name[n] = ListB[i]

                n += 1

        # 初始化每本书籍与自己相关联，f[i] = i

        f = [i for i in range(0, n+1)]

        # 并查集合并操作，将有关联的两本书籍进行关系连接操作

        for i in range(0, len(ListA)):

            x, y = self.find(digit[ListA[i]], f), self.find(digit[ListB[i]], f)

            if x != y:

                f[y] = x

        # 找出最大的关联集合

        now_sum = [0]*n

        max_id, max_sum = 0, 0

        for i in range(0, n):

            f[i] = self.find(i, f)

            now_sum[f[i]] += 1

            if now_sum[f[i]] > max_sum:

                max_id = f[i]

                max_sum = now_sum[f[i]]

        # 将数字重新转换为书籍名字

        res = []

        for i in range(0, n):

            if f[i] == max_id:

                res.append(name[i])

        return res
```