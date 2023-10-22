---
title: 81. Search in Rotated Sorted Array II
description: use binary search, take in consider potential offset, skip the same values
date: 2023-10-22
tags: [ binary-search, medium ] 
---

```python
# O(log(n)) time || O(1) space
def search(self, nums: List[int], target: int) -> bool:
    low, high = 0, len(nums) - 1
    while low <= high:
        mid = low + (high - low) // 2

        if target == nums[mid]:
            return True

        while low < mid and nums[low] == nums[mid]:
            low += 1

        if nums[low] <= nums[mid]:
            if nums[low] <= target <= nums[mid]:
                high = mid - 1
            else:
                low = mid + 1
        else:
            if nums[mid] <= target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1

    return False
```

array might be offset but still is sorted. \
use binary search, take in consider in which part to have a search. \
skip the same values if `low` is less `mid`
