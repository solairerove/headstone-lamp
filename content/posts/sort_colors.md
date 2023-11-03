---
title: 75. Sort Colors
description: This is the famous "Dutch National Flag" problem.
date: 2023-11-02
tags: [ arrays, two-pointers, sorting, medium ]
---

```python
# O(n) time || O(1) space
def sort_colors(self, nums: List[int]) -> None:
    lt, i, gt = 0, 0, len(nums) - 1
    while i <= gt:
        if nums[i] == 0:
            nums[i], nums[lt] = nums[lt], nums[i]
            i, lt = i + 1, lt + 1
        elif nums[i] == 2:
            nums[i], nums[gt] = nums[gt], nums[i]
            gt -= 1
        else:
            i += 1
```

This is the famous "Dutch National Flag" problem. One common way to solve this problem is using a three-pointer
approach. The idea is to use one pointer to separate the 0s, one to separate the 2s, and one to iterate through the
array.

Here's a step-by-step explanation of the algorithm:

1) Initialize three pointers: `left`, `current`, and `right`.
2) `left` will be the position where we'll place the next 0 we encounter.
3) `right` will be the position where we'll place the next 2 we encounter.
4) `current` will iterate through the entire array.
5) If `nums[current]` is 0, we swap the elements at `current` and `left`, increment both `left` and `current`.
6) If `nums[current]` is 2, we swap the elements at `current` and `right`, and then decrement `right`. Note that we
   don't increment current here because the swapped element from the right could be 0 or 1 or 2.
7) If `nums[current]` is 1, we just increment `current`.
