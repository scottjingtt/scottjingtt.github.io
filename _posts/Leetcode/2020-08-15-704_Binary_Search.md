---
layout:     post
title:      "Leetcode: 704. Binary Search"
subtitle:   " 704. Binary Search"
date:       2020-08-15 01:18:00
author:     "Scott"
header-img: "img/posts/post-bg-20191125.jpg"
catalog: true
mathjax: true
header-mask: 0.3
tags:
    - Leetcode
    - Binary Search
---




## 704. Binary Search
Given a sorted (in ascending order) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.

Example:
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

**Note**:

You may assume that all elements in nums are unique.
n will be in the range [1, 10000].
The value of each element in nums will be in the range [-9999, 9999].

### *Solution 1*
***Thinking***: Recursion

Time Complexity: $O(log n)$

Space Complexity: $O(1)$

### <font color='green'>Accepted</font> 
Runtime: $< 22.97\%$

Memory Usage: $< 11.76\%$

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if nums == None or len(nums) == 0:
            return -1
        
        return self.search_subarray(nums, target, 0, len(nums)-1)
        
    def search_subarray(self, nums: List[int], target: int, start_idx: int, end_idx: int) -> int:
        if start_idx > end_idx:
            return -1
        if start_idx == end_idx:
            if nums[start_idx] == target:
                return start_idx
            else:
                return -1
        
        mid_idx = start_idx + (end_idx - start_idx) // 2
        if nums[mid_idx] == target:
            return mid_idx
        elif nums[mid_idx] < target:
            start_idx = mid_idx + 1
            return self.search_subarray(nums, target, start_idx, end_idx)
        elif nums[mid_idx] > target:
            end_idx = mid_idx - 1
            return self.search_subarray(nums, target, start_idx, end_idx)
        else:
            raise Exception("Error")
```
### Notes: 
1. If start_idx = mid_idx + 1 and end_idx = mid_idx -1, then only need to check when 1 element in the nums at the end, aka ```start_idx == end_idx```

### *Solution 2*
***Thinking***: Recursion

Time Complexity: $O(log n)$

Space Complexity: $O(1)$

### <font color='green'>Accepted</font> 
Runtime: $< 74.81\%$

Memory Usage: $< 73.36\%$

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if nums == None or len(nums) == 0:
            return -1
        
        return self.search_subarray(nums, target, 0, len(nums)-1)
        
    def search_subarray(self, nums: List[int], target: int, start_idx: int, end_idx: int) -> int:
        if start_idx > end_idx:
            return -1
        elif end_idx - start_idx <= 1:
            if nums[start_idx] == target:
                return start_idx
            elif nums[end_idx] == target:
                return end_idx
            else:
                return -1
        else:
            pass

        mid_idx = start_idx + (end_idx - start_idx) // 2
        if nums[mid_idx] == target:
            return mid_idx
        elif nums[mid_idx] < target:
            start_idx = mid_idx
            return self.search_subarray(nums, target, start_idx, end_idx)
        elif nums[mid_idx] > target:
            end_idx = mid_idx
            return self.search_subarray(nums, target, start_idx, end_idx)
        else:
            raise Exception("Error")
```
### Notes: 
1. If start_idx and end_idx do not add/minus 1 to mid_idx, which is ``` start_idx = mid_idx or end_idx = mid_idx ```, so need to check the situation when 2 elements in the nums.


### *Solution 3*
***Thinking***: Iteration

Time Complexity: $O(log n)$

Space Complexity: $O(1)$

### <font color='green'>Accepted</font> 
Runtime: $< 63.29\%$

Memory Usage: $< 73.36\%$

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if nums == None or len(nums) == 0:
            return -1
        
        return self.search_subarray(nums, target)
        
    def search_subarray(self, nums: List[int], target: int) -> int:
        start_idx = 0
        end_idx = len(nums) - 1
        
        while start_idx <= end_idx:
            if nums[start_idx] == target:
                return start_idx
            elif nums[end_idx] == target:
                return end_idx
            else:
                mid_idx = start_idx + (end_idx - start_idx) // 2
                if nums[mid_idx] == target:
                    return mid_idx
                elif nums[mid_idx] < target:
                    start_idx = mid_idx + 1
                    continue
                else: # nums[mid_idx] > target:
                    end_idx = mid_idx - 1
                    continue
        return -1
```
### Notes: 
1. If start_idx = mid_idx + 1 and end_idx = mid_idx -1, then only need to check when 1 element in the nums at the end, aka ```start_idx == end_idx```.