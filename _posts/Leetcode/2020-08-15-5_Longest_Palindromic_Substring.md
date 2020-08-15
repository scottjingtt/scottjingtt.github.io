---
layout:     post
title:      "Leetcode: 5. Longest Palindromic Substring"
subtitle:   " 5. Longest Palindromic Substring"
date:       2020-08-15 00:22:00
author:     "Scott"
header-img: "img/posts/post-bg-20191125.jpg"
catalog: true
mathjax: true
header-mask: 0.3
tags:
    - Leetcode
    - String
---




## 5. Longest Palindromic Substring
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.


Example:
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Input: "cbbd"
Output: "bb"
```


### *Solution 1*
***Thinking***:  Traverse all characters as "MIDDLE" or "LEFT & RIGHT"

Time Complexity: $O(n^2)$

Space Complexity: $O(1)$

### <font color='green'>Accepted</font> 
Runtime: $<69.44\%$

Memory Usage: $<52.34\%$

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if s is None:
            return None
        if len(s) == 0 or len(s) == 1:
            return s
        
        result = ''
        pal_length = 0
        
        # s[i] as the middle
        for i in range(len(s)):
            mid_idx = i
            left_idx = i - 1
            right_idx = i + 1
            pal_length = 1
            while left_idx >= 0 and right_idx < len(s):
                if s[left_idx] == s[right_idx]:
                    pal_length += 2
                    left_idx -= 1
                    right_idx += 1
                else:
                    break
            left_idx += 1
            right_idx -= 1
                    
            if pal_length > len(result):
                result = s[left_idx : right_idx+1]
            
        # s[i] is left, s[i+1] is right
        for j in range(len(s)):
            left_idx = j
            right_idx = j + 1
            pal_length = 0
            while left_idx >= 0 and right_idx < len(s):
                if s[left_idx] == s[right_idx]:
                    pal_length += 2
                    left_idx -= 1
                    right_idx += 1
                else:
                    break
            left_idx += 1
            right_idx -= 1
            if pal_length > len(result):
                result = s[left_idx: right_idx+1]
                # print("(2)", i, result)
                
        return result
```
### Notes: 
1. Be carefull about the index, especially when the "if s[left] == s[right]", and "while left/right border", once breaks the rule, remember to left ++, and right --
2. Remember to result substring, instead of length