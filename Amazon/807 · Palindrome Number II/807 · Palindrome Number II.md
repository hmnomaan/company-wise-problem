### 807 · Palindrome Number II
Algorithms
Easy
Accepted Rate
52%



### Description
Determines whether a binary representation of a non-negative integer n is a palindrome

## (i) 
0 <= n <= 2^32 - 1


## Example
1
```python
Input: n = 0
Output: True
Explanation:
The binary representation of 0 is: 0

```
2
```python
Input: n = 3
Output: True
Explanation:
The binary representation of 3 is: 11

```
3
```python
Input: n = 4
Output: False
Explanation:
The binary representation of 4 is: 100

```
4
```python
Input: n = 6
Output: False
Explanation:
The binary representation of 6 is: 110

```
### SOLVE this:

```python
class Solution:
    """
    @param n: non-negative integer n.
    @return: return whether a binary representation of a non-negative integer n is a palindrome.
    """
    def is_palindrome(self, n: int) -> bool:
        # Write your code here

```

### Tags
Enumerate
Simulation



## Company
Amazon

### Related Problems

Related Problems

745
Palindromic Ranges
Medium

775
Palindrome Pairs
Hard

807
Palindrome Number II
Easy

1735
Super Palindromes
Hard




### best answer
```py
class Solution:
    """
    @param n: non-negative integer n.
    @return: return whether a binary representation of a non-negative integer n is a palindrome.
    """
    def is_palindrome(self, n: int) -> bool:
        # Write your code here
        binary = bin(n)[2:]  # 将整数转换为二进制字符串，并去掉前缀 '0b'
        return binary == binary[::-1]  # 检查二进制字符串是否为回文
#转换为二进制字符串：bin(n) 将整数转换为二进制字符串，返回的字符串以 '0b' 开头。
#使用 [2:] 切片去掉前缀，得到纯二进制字符串。
#回文检查：binary[::-1] 生成字符串的反向版本，通过比较原字符串和反向字符串是否相等来判断是否为回文。
        
```
```py
class Solution:
    """
    @param n: non-negative integer n.
    @return: return whether a binary representation of a non-negative integer n is a palindrome.
    """
    def isPalindrome(self, n):
        if n is None:
            return False
        num = bin(n)[2:]
        l, r = 0, len(num) - 1
        while l < r:
            if num[l] != num[r]:
                return False
            l += 1
            r -= 1
        
        return True
    
    
    # def isPalindrome(self, n):
    #     if n is None: #cannot use not n since not 0 is True
    #         return False
        
    #     num = bin(n)[2:]
    #     for i in range(len(num) // 2 + 1): #add 1 is used for special case number 0 should be true
    #         if num[i] != num[-i - 1]:
    #             print(num[i], num[-i - 1])
    #             return False
        
    #     return True
```


### Official answer from lintcode

```py
class Solution:
    """
    @param n: non-negative integer n.
    @return: return whether a binary representation of a non-negative integer n is a palindrome.
    """
    def isPalindrome(self, n):
        # write code here.
        num = bin(n)[2:]
        for i in range(len(num)):
            if num[i] != num[-i - 1]:
                return False
        return True
```