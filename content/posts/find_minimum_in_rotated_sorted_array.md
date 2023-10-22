---
title: 153. Find Minimum in Rotated Sorted Array
description: use binary search, if mid element bigger than last, we know borders
date: 2023-10-22
tags: [ binary-search, medium ] 
---

```python
# O(log(n)) time || O(1) space
def find_min(self, nums: List[int]) -> int:
    low, high = 0, len(nums) - 1
    while low < high:
        mid = low + (high - low) // 2
        if nums[mid] > nums[high]:
            low = mid + 1
        else:
            high = mid

    return nums[high]
```

array might be offset but still is sorted. \
use binary search, take in consider in which part to have a search. \
if mid element bigger than last one, `low` border is `mid + 1` 
