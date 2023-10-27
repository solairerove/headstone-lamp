---
title: 977. Squares of a Sorted Array
description: use two pointers and compare left and right num using abs
date: 2023-10-26
tags: [ arrays, two-pointers, easy ]
---

```python
# O(n) time || O(1) space
def sorted_squares(self, nums: List[int]) -> List[int]:
    res = [0] * len(nums)
    pos = len(nums) - 1
    low, high = 0, len(nums) - 1
    while low <= high:
        if abs(nums[low]) > abs(nums[high]):
            res[pos] = nums[low] ** 2
            low += 1
        else:
            res[pos] = nums[high] ** 2
            high -= 1
        pos -= 1

    return res
```

Given that the array is sorted in non-decreasing order, the negative numbers will be on the left side and the positive
numbers on the right. Squaring the numbers can reverse the order for negative numbers, as larger negative numbers will
result in larger squares.

The approach here is to use two pointers technique. One pointer starts at the beginning of the array and the other at
the end. We compare the absolute values of the numbers at these pointers, square the larger absolute value, and place it
at the current position in our result array (starting from the end). Then, depending on which number we squared, we move
the corresponding pointer.
