---
layout:     post
title:      "Leetcode: 409. Longest Palindrome"
subtitle:   " 409. Longest Palindrome"
date:       2020-08-15 01:18:00
author:     "Scott"
header-img: "img/posts/post-bg-20191125.jpg"
catalog: true
mathjax: true
header-mask: 0.3
tags:
    - Leetcode
    - String
---




## 409. Longest Palindrome
Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

**Note**:
Assume the length of given string will not exceed 1,010. 

Example:
```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```


### *Solution 1*
***Thinking***: Use hash map to calculate all characters, and calculate how many EVEN numver of pairs can construct, additional Single center character if there are some unused character left.

Time Complexity: $O(n)$

Space Complexity: $O(n)$

### <font color='green'>Accepted</font> 
Runtime: $< 90.97\%$

Memory Usage: $< 54.89\%$

```python
class Solution:
    def longestPalindrome(self, s: str) -> int:
        if s is None:
            return 0
        if len(s) == 0 or len(s) == 1:
            return len(s)
        
        char_cnt = {}
        for i in range(len(s)):
            c = s[i]
            if c not in char_cnt:
                char_cnt[c] = 1
            else:
                char_cnt[c] += 1
        
        result = 0
        for i, (c, n) in enumerate(char_cnt.items()): # for key in char_cnt:
            result += (n // 2 * 2)
            # print(c, n,n//2)
        
        if result < len(s):
            result = result + 1
        else:
            result = result
        return result
```
### Notes: 
1. Be careful about the "result *2", because TWO same character can consist one pair with length 2!