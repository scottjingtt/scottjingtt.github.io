---
layout:     post
title:      "Leetcode: 125. Valid Palindrome"
subtitle:   " 125. Valid Palindrome"
date:       2020-08-15 01:05:00
author:     "Scott"
header-img: "img/posts/post-bg-20191125.jpg"
catalog: true
mathjax: true
header-mask: 0.3
tags:
    - Leetcode
    - String
---




## 125. Valid Palindrome
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note**: For the purpose of this problem, we define empty string as valid palindrome.

Example:
```
Input: "A man, a plan, a canal: Panama"
Output: true

Input: "race a car"
Output: false
```
**Constraints**:

- s consists only of printable ASCII characters.


### *Solution 1*
***Thinking***: Find the middle and dicide the start left/right indexes, then compare all LEFT and RIGHT characters until the end of the string

Time Complexity: $O(n)$

Space Complexity: $O(n)$

### <font color='green'>Accepted</font> 
Runtime: $< 81.61\%$

Memory Usage: $< 94.00\%$

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        if s is None:
            return False
        elif len(s) == 0 or len(s) == 1:
            return True
        
        # Remove space and other symbols, only keep lower case alphabats
        new_alpha = ''
        for c in s.lower():
            if c.isalnum():   #string.isalpha(),  string.isalnum()
                new_alpha = new_alpha + c
        print(new_alpha)
        
        # find middle c, and left & right start idx
        if len(new_alpha) % 2 == 0:
            left_idx = len(new_alpha) //2 - 1
            right_idx = len(new_alpha) // 2
        else:
            mid_idx = len(new_alpha) // 2
            left_idx = mid_idx - 1
            right_idx = mid_idx + 1
        
        # check if palindrome
        while left_idx >= 0 and right_idx < len(new_alpha):
            # print(left_idx, right_idx, new_alpha[left_idx], new_alpha[right_idx])
            if new_alpha[left_idx] == new_alpha[right_idx]:
                left_idx -= 1
                right_idx += 1
            else:
                return False
        
        return True
```
### Notes: 
1. Cleasing the string:  
	string.isalpha(): check if is alpha character

	string.isalnum(): check if is alpha or number (alphnumeric)
2. Be carefull!!! Use the new alphanumeric only string! instead of the input string