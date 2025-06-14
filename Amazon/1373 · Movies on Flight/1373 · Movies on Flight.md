### 1373 · Movies on Flight
Algorithms
Medium
Accepted Rate
47%


### Description
You are on a flight and wanna watch two movies during this flight.
You are given an array movieDurations which includes all the movie durations.
You are also given the duration of the flight which is k minutes.
Now, you need to pick two movies and the total duration of the two movies is less than or equal to (k - 30min).

Find the pair of movies with the longest total duration and return their indexes. If multiple found, he pair with the largest duration of a single movie.




## Example
```python
Example:
Input: movieDurations = [90, 85, 75, 60, 120, 150, 125], d = 250
Output: [0, 6]
Explanation: movieDurations[0] + movieDurations[6] = 90 + 125 = 215 is the maximum number within 220 (250min - 30min)

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
    @param arr: An integer array represents durations of movies
    @param k: An integer represents the duration of the flight
    @return: the pair of movies index with the longest total duration
    """
    def flight_details(self, arr: List[int], k: int) -> List[int]:
        # write your code here

```

### Tags
Opposite Direction Two Pointers
Two Pointers

## Company
Amazon
Google
### Related Problems






### best answer
```py
class Solution:
    """
    @param arr: An integer array
    @param k: An integer
    @return: return the pair of movies index with the longest total duration
    """
    def FlightDetails(self, arr, k):
        # write your code here
        if not arr:
            return []
            
        if len(arr) == 1:
            if arr[0] < k:
                return [0]
            return []
            
        index_map = {}
        for i in range(len(arr)):
            index_map[arr[i]] = i
            
        arr.sort()
        i, j = 0, len(arr) - 1
        max_duriation = 0
        res = []
        while i < j:
            duriation = arr[i] + arr[j]
            if duriation == k - 30:
                return [index_map[arr[i]], index_map[arr[j]]]
            if duriation < k - 30:
                if duriation > max_duriation:
                    max_duriation = duriation
                    res = [index_map[arr[i]], index_map[arr[j]]]
                i += 1
            else:
                j -= 1
        return sorted(res)
```
```py
class Solution:
    """
    @param arr: An integer array
    @param k: An integer
    @return: return the pair of movies index with the longest total duration
    """
    def FlightDetails(self, arr, k):
        if len(arr) < 2:
            return None
        duration_to_index = {v: k for k, v in enumerate(arr)}
        arr.sort()
        cap = k - 30
        max_total = 0
        max_pair = [None, None]
        left, right = 0, len(arr) - 1
        while left < right:
            current_total = arr[left] + arr[right]
            if current_total > cap:
                right -= 1
                continue
            if current_total > max_total:
                max_total = current_total
                max_pair = [arr[left], arr[right]]
            left += 1
        if max_pair == [None, None]:
            return None
        indices = [duration_to_index[max_pair[0]], duration_to_index[max_pair[1]]]
        indices.sort()
        return indices


"""
movieDurations = [90, 85, 75, 60, 120, 150, 125], d = 250
d -30 = 220
{v:k for k, v in enumerate(arr)}
arr.sort()
60 75 85 90 120 125 150
max_total made_with
210    60 150    good
225    75 150    no good
200    75 125    good
210    85 125    good
215    90 125    good
245    120 125   no good    stop

only when total > max_total, update max_total

"""
```


### Official answer from lintcode
Double pointer
```py
class Solution:
    """
    @param arr: An integer array
    @param k: An integer
    @return: return the pair of movies index with the longest total duration
    """
    def FlightDetails(self, arr, k):
        durations = []
        for i, duration in enumerate(arr):
            durations.append((duration, i))
        durations.sort()
        start = 0
        end = len(durations) - 1
        target = k - 30

        result_index = None
        result_duration = 0
        while start < end:
            duration = durations[start][0] + durations[end][0]
            if duration <= target:
                if target - duration < target - result_duration:
                    result_index = (start, end)
                    result_duration = duration
                start += 1
            else:
                end -= 1
        return sorted([durations[result_index[0]][1], durations[result_index[1]][1]])
```