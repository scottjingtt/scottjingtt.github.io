---
layout:     post
title:      "Leetcode: 28. Implement strStr()"
subtitle:   " 28. Implement strStr()"
date:       2020-08-15 00:53:00
author:     "Scott"
header-img: "img/posts/post-bg-20191125.jpg"
catalog: true
mathjax: true
header-mask: 0.3
tags:
    - Leetcode
    - String
---




## 28. Implement strStr()
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example:
```
Input: haystack = "hello", needle = "ll"
Output: 2

Input: haystack = "aaaaa", needle = "bba"
Output: -1
```


### *Solution 1*
***Thinking***: To limit the time complexity, don't need to check all characters in the haystack, just when the left substring length is shorter than the needle length, can stop there. 

Time Complexity: $O(N*M)$, where N is the string length, M is the needle length

Space Complexity: $O(1)$

### <font color='green'>Accepted</font> 
Runtime: 36 ms

Memory Usage: 13.8 MB

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if haystack is None:
            return -1
        if needle == '':
            return 0
        
        result = -1
        for i in range(len(haystack)):
            result = i
            for j in range(len(needle)):
                if i+j >= len(haystack) or needle[j] != haystack[i+j]:
                    result = -1
                    break
                else:
                    continue
            
            if result != -1 or len(haystack) - i < len(needle):
                break
            else:
                continue
        
        return result
```
### Notes: 
1. Because need to use i+j, so MUST check if it is out if index limit
2. Note: len(string) - start_idx   <==> end_idx - start_idx + 1