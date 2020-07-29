---
layout:     post
title:      "Leetcode: 35. Search Insert Position"
subtitle:   " 35. Search Insert Position"
date:       2020-07-29 00:35:00
author:     "Scott"
header-img: "img/posts/post-bg-20191125.jpg"
catalog: true
mathjax: true
header-mask: 0.3
tags:
    - Leetcode
    - Binary Search
---




## 35. Search Insert Position
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example:
```
Input: [1,3,5,6], 5
Output: 2

Input: [1,3,5,6], 2
Output: 1

Input: [1,3,5,6], 7
Output: 4

Input: [1,3,5,6], 0
Output: 0
```


### *Solution 1* - Loop all elements
***Thinking***: Traverse all elements and check if it equal to the target. 

Time Complexity: $O(n)$

Space Complexity: $O(1)$

### <font color='green'>Success</font> 

Runtime: **36** ms

Memory Usage: **14.7** MB

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        if nums is None:
            return null
        if len(nums) == 0:
            return 0
        
        for i in range(len(nums)):
            if target <= nums[i]:
                return i
        return len(nums)
```

### *Solution 2* - Binary Search
***Thinking***: Binary search insteaf of looping all elements. 

Time Complexity: $O(log \,\, n)$

Space Complexity: $O(1)$

### <font color='green'>Success</font> 

Runtime: **48** ms

Memory Usage: **14.5** MB, 

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        if nums is None:
            return null
        if len(nums) == 0:
            return 0
        
        start = 0
        end = len(nums)-1
        while start+1 < end:
            mid = start + (end-start)//2
            mid_val = nums[mid]
            if mid_val == target:
                return mid
            elif mid_val > target:
                end = mid
            else:
                start = mid
                
        if nums[start] >= target:
            return start
        elif nums[end] >= target:
            return end
        else:
            return end+1
```
--- 
