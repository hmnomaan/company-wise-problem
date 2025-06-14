### 1380 · Log Sorting
Algorithms
Easy
Accepted Rate
50%


### Description
Given a list of string logs, in which each element representing a log. Each log can be separated into two parts by the first space. The first part is the ID of the log, while the second part is the content of the log. (The content may contain spaces as well.) The content is composed of only letters and spaces, or only numbers and spaces.

Now you need to sort logs by following rules:

1. Logs whose content is letter should be ahead of logs whose content is number.
2. Logs whose content is letter should be sorted by their content in lexicographic order. And when two logs have same content, sort them by ID in lexicographic order.
3. Logs whose content is number should be in their input order.

## (i)
1. The total number of logs will not exceed 5000
2. The length of each log will not exceed 100
3. Ensure that there are no duplicate IDs + content


## Example
1
```python
Input:  
    logs = [
        "zo4 4 7",
        "a100 Act zoo",
        "a1 9 2 3 1",
        "g9 act car"
    ]
Output: 
    [
        "a100 Act zoo",
        "g9 act car",
        "zo4 4 7",
        "a1 9 2 3 1"
    ]
Explanation: "Act zoo" < "act car", so the output is as above.

```
2
```python
Input:  
    logs = [
        "zo4 4 7",
        "a100 Actzoo",
        "a100 Act zoo",
        "Tac Bctzoo",
        "Tab Bctzoo",
        "g9 act car"
    ]
Output: 
    [
        "a100 Act zoo",
        "a100 Actzoo",
        "Tab Bctzoo",
        "Tac Bctzoo",
        "g9 act car",
        "zo4 4 7"
    ]
Explanation:
    Because "Bctzoo" == "Bctzoo", the comparison "Tab" and "Tac" have "Tab" < Tac ", so" Tab Bctzoo "< Tac Bctzoo".
    Because ' '<'z', so "A100 Act zoo" < A100 Actzoo".

```
### SOLVE this:

```python
from typing import (
    List,
)

class Solution:
    """
    @param logs: the logs
    @return: the logs after sorting
    """
    def log_sort(self, logs: List[str]) -> List[str]:
        # Write your code here

```

### Tags
String
Sort

## Company
Amazon

### Related Problems






### best answer
1
```py
from typing import (
    List,
)

class Solution:
    """
    @param logs: the logs
    @return: the logs after sorting
    """
    def log_sort(self, logs: List[str]) -> List[str]:
        # Write your code here
        return sorted(logs, key=self.sort_id)

    
    def sort_id(self, log: str) -> tuple:
        a, b = log.split(" ", 1)
        return (0, b, a) if b[0].isalpha() else (1,)


```
2
```py
from typing import (
    List,
)

class Solution:
    """
    @param logs: the logs
    @return: the logs after sorting
    """
    def log_sort(self, logs: List[str]) -> List[str]:
        Nums=[]
        Wrds=[]
        for log in logs:
            if log.split(' ')[-1].isdigit():
                Nums.append(log)
            else:
                Wrds.append(log)
        
        return sorted(Wrds, key=self.mykeys) + Nums # key，函数无输入
    
    def mykeys(self, log): # 比较函数, 输入为每个元素
        pos=log.index(' ')
        return (log[pos+1:],log[:pos]) # 元组形式，按排列优先级顺序
```
3
```py
class Solution:
    """
    @param logs: the logs
    @return: the logs after sorting
    """
    def logSort(self, logs):
        # Write your code here
        letter_logs = []
        result = []
        for log in logs:
            log_id, content = log.split(maxsplit=1)
            if content[0].isdigit():
                result.append(log)
            else:
                letter_logs.append((content, log))
        
        result = [letter_log[1] for letter_log in sorted(letter_logs)] + result
        return result
```


### Official answer from lintcode
自定义排序
思路

根据题意自定义排序的比较方式。比较时，先将数组日志按照第一个空格分成两部分字符串，其中第一部分为标识符。第二部分的首字符可以用来判断该日志的类型。两条日志进行比较时，需要先确定待比较的日志的类型，然后按照以下规则进行比较：

字母日志始终小于数字日志。
数字日志保留原来的相对顺序。当使用稳定的排序算法时，可以认为所有数字日志大小一样。当使用不稳定的排序算法时，可以用日志在原数组中的下标进行比较。
字母日志进行相互比较时，先比较第二部分的大小；如果相等，则比较标识符大小。比较时都使用字符串的比较方式进行比较。
定义比较函数 
logCompare
logCompare 时，有两个输入 
log
1
log 
1
​
  和 
log
2
log 
2
​
  。当相等时，返回 
0
0；当 
log
1
log 
1
​
  大时，返回正数；当 
log
2
log 
2
​
  大时，返回负数。

  Custom sorting Ideas Customize the sorting comparison method according to the question. When comparing, first divide the array log into two strings according to the first space, where the first part is the identifier. The first character of the second part can be used to determine the type of the log. When comparing two logs, you need to first determine the type of the log to be compared, and then compare them according to the following rules: The letter log is always smaller than the digital log. The digital log retains the original relative order. When using a stable sorting algorithm, it can be assumed that all digital logs have the same size. When using an unstable sorting algorithm, the log's subscript in the original array can be used for comparison. When comparing letter logs, first compare the size of the second part; if they are equal, compare the size of the identifier. When comparing, use the string comparison method for comparison. When defining the comparison function logCompare logCompare, there are two inputs log 1 log 1​and log 2 log 2​. When they are equal, return 0 0; when log 1 log 1​is greater, return a positive number; when log 2 log 2​is greater, return a negative number.
  
   Code
```py
from typing import (
    List,
)
class Solution:
    def log_sort(self, logs: List[str]) -> List[str]:
        def trans(log: str) -> tuple:
            a, b = log.split(' ', 1)
            return (0, b, a) if b[0].isalpha() else (1,)

        logs.sort(key=trans)  # sort 是稳定排序
        return logs

```
//
Complexity Analysis Time complexity: 𝑂 ( 𝑛 log ⁡ 𝑛 ) O(nlogn), where 𝑛 n is the number of characters in logs logs, and is the time complexity of the built-in sort in the average case. Space complexity: 𝑂 ( 𝑛 ) O(n) or 𝑂 ( 1 ) O(1) (depending on the language implementation). A new array needs to be created to store log log and subscripts, and each log log needs to be split.
//

2
//
Classify the logs by whether the content is numeric or alphabetical, and then sort the alphabetical ones by (content, ID). Then connect the sorted ones with the numeric ones.
```py
class Solution:
    """
    @param logs: the logs
    @return: the log after sorting
    """
    def logSort(self, logs):
        withInt = []
        withStr = []
        for i in logs:
            if i.split(' ')[-1].isdigit():
                withInt.append(i)
            else:
                withStr.append(i)
        
        return sorted(withStr, key = Solution.mykey) + withInt
    
    @staticmethod
    def mykey(x):
        pos = x.index(' ')
        return (x[pos+1:], x[:pos])
```
