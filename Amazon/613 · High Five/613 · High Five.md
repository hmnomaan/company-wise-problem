###  613 · High Five
Algorithms
Medium
Accepted Rate
46%

### Description
Each student has two attributes ID and scores. Find the average of the top five scores for each student.
## Example

Example 1:
```python
Input: 
[[1,91],[1,92],[2,93],[2,99],[2,98],[2,97],[1,60],[1,58],[2,100],[1,61]]
Output:
1: 72.40
2: 97.40

```
Example 2:
```python
Input:
[[1,90],[1,90],[1,90],[1,90],[1,90],[1,90]]
Output: 
1: 90.00

```
### Solve this
```python
'''
Definition for a Record
class Record:
    def __init__(self, id, score):
        self.id = id
        self.score = score
'''
class Solution:
    # @param {Record[]} results a list of <student_id, score>
    # @return {dict(id, average)} find the average of 5 highest scores for each person
    # <key, value> (student_id, average_score)
    def highFive(self, results):
        # Write your code here

```






### Tags
Tags
Hash Table
Heap


## Company
Amazon

### Related Problems
Related Problems

544
Top k Largest Numbers
Medium





### best answer

```py
'''
Definition for a Record
class Record:
    def __init__(self, id, score):
        self.id = id
        self.score = score
'''
import heapq
class Solution:
    # @param {Record[]} results a list of <student_id, score>
    # @return {dict(id, average)} find the average of 5 highest scores for each person
    # <key, value> (student_id, average_score)
    def highFive(self, results):
        # Write your code here
        dicts = {}
        for record in results:
            sid = record.id
            grade = record.score
            if sid not in dicts:
                dicts[sid] = []
                heapq.heappush(dicts[sid],grade)
            else:
                heapq.heappush(dicts[sid],grade)
            if len(dicts[sid]) > 5:
                heapq.heappop(dicts[sid])
        
        result = {}        
        for sid in dicts:
            grades = [grade for grade in dicts[sid]]
            result[sid] = self.getavg(grades)
        return result
            
    
    
    def getavg(self,grades):
        sums  = sum(grades)
        return sums/ len(grades)
```
```py
'''
Definition for a Record
class Record:
    def __init__(self, id, score):
        self.id = id
        self.score = score
'''

import heapq
class Solution:
    # @param {Record[]} results a list of <student_id, score>
    # @return {dict(id, average)} find the average of 5 highest scores for each person
    # <key, value> (student_id, average_score)
    def highFive(self, results):
        # Write your code here
        record = {}
        for result in results:
            id, score = result.id, result.score
            if id not in record:
                record[id] = []
            heapq.heappush(record[id], score)
            if len(record[id]) > 5:
                heapq.heappop(record[id])
        ans = {}
        for k, v in record.items():
            ans[k] = sum(v) / len(v)
        
        return ans
```

### Official answer from lintcode
Use map to find the corresponding person's score, and then brute force compare the top 5.
```py
class Solution:
    # @param {Record[]} results a list of <student_id, score>
    # @return {dict(id, average)} find the average of 5 highest scores for each person
    # <key, value> (student_id, average_score)
    def highFive(self, results):
        # Write your code here
        hash = dict()
        for r in results:
            if r.id not in hash:
                hash[r.id] = []

            hash[r.id].append(r.score)
            if len(hash[r.id]) > 5:
                index = 0
                for i in xrange(1, 6):
                    if hash[r.id][i] < hash[r.id][index]:
                        index = i

                hash[r.id].pop(index)

        answer = dict()
        for id, scores in hash.items():
            answer[id] = sum(scores) / 5.0

        return answer
```