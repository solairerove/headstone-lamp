---
title: 704. Binary Search
description: on each iteration decrease search space in two times
date: 2023-10-20
tags: [ binary-search, easy ] 
---

```python
# O(log(n)) time || O(1) space
def search(self, nums: List[int], target: int) -> int:
    low, high = 0, len(nums) - 1
    while low <= high:
        mid = low + (high - low) // 2
        if target == nums[mid]:
            return mid
        elif target < nums[mid]:
            high = mid - 1
        else:
            low = mid + 1

    return -1
```

classic default binary search. \
have two pointers as search border. \
decrease search borders two times on each iteration like you're trying to find word in dictionary book.
