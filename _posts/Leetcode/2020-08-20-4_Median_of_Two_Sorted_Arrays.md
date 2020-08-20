---
layout:     post
title:      "Leetcode: 4. Median of Two Sorted Arrays"
subtitle:   " 704. Binary Search"
date:       2020-08-20 13:33:00
author:     "Scott"
header-img: "img/posts/post-bg-20191125.jpg"
catalog: true
mathjax: true
header-mask: 0.3
tags:
    - Leetcode
    - Binary Search
---




## 4. Median of Two Sorted Arrays
Given two sorted arrays nums1 and nums2 of size m and n respectively.

Return the median of the two sorted arrays.

Follow up: The overall run time complexity should be O(log (m+n)).


Example:
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.

Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

Input: nums1 = [0,0], nums2 = [0,0]
Output: 0.00000

Input: nums1 = [], nums2 = [1]
Output: 1.00000

Input: nums1 = [2], nums2 = []
Output: 2.00000

```

<!-- **Note**: -->

**Constraints**:

    nums1,length == m
    nums2,length == n
    0 <= m <= 1000
    0 <= n <= 1000
    1 <= m + n <= 2000


### *Solution 1*
***Thinking***: If no time cmoplexity constraint, apply **Merge Sort** to get the K-th element.

Time Complexity: $O(m + n)$

Space Complexity: $O(1)$

### *Solution 2*
***Thinking***: **Binary Search** - eliminate half each recursion.

Time Complexity: $O(log(m + n))$

Space Complexity: $O(1)$

### <font color='green'>Accepted</font> 
Runtime: $< 25.13\%$

Memory Usage: $< 24.05\%$

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        
        len1 = len(nums1)
        len2 = len(nums2)
        
        if (len1 + len2) % 2 == 0:
            k = (len1 + len2) // 2
            return (self.findKth(nums1, nums2, k) + self.findKth(nums1, nums2, k - 1)) / 2
        else: # (len1 + len2) % 2 == 1:
            k = (len1 + len2) // 2
            return self.findKth(nums1, nums2, k)
            
            
    
    def findKth(self, nums1: List[int], nums2: List[int], K: int) -> float:
        print("nums1: ", nums1)
        print("nums2: ", nums2)
        print("K: ", K)
        if (not nums1) or len(nums1) == 0:
            return nums2[K]
        if (not nums2) or len(nums2) == 0:
            return nums1[K]
        
        mid_idx1 = len(nums1) // 2
        mid_idx2 = len(nums2) // 2
        
        if K > (mid_idx1 + mid_idx2):
            if nums1[mid_idx1] > nums2[mid_idx2]:
                return self.findKth(nums1, nums2[mid_idx2 + 1 : ], K - mid_idx2 - 1)
            else:
                return self.findKth(nums1[mid_idx1 + 1 : ], nums2, K - mid_idx1 - 1)
        else:
            if nums1[mid_idx1] > nums2[mid_idx2]:
                return self.findKth(nums1[ : mid_idx1], nums2, K)
            else:
                return self.findKth(nums1, nums2[ : mid_idx2], K)
```
### Notes: 
1. Need to check the remain subarrays **length** with the **K**, check if ``` K < (mid_idx1 + mid_idx2)```, remove the last half and still look for the **K-th**. Otherwise, if ```K >= (mid_idx1 + mid_idx2)```, remove the first half and change to look for the **K - mid_idx? - 1** element in the remain arrays. 
2. Then check the medians of the two arrays, ``` nums1[mid_idx1], nums2[mid_idx2] ```.
