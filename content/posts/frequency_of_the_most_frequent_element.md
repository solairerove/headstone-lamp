---
title: 1838. Frequency of the Most Frequent Element
description: find the longest subarray in which the difference between the max and min
date: 2023-11-18
tags: [ sliding-window, arrays, medium ]
---

```python
# O(n * log(n)) time | O(log(n)) space
def max_frequency(self, nums: List[int], k: int) -> int:
    nums.sort()
    low, res, total = 0, 0, 0
    for high in range(len(nums)):
        total += nums[high]

        while nums[high] * (high - low + 1) - total > k:
            total -= nums[low]
            low += 1

        res = max(res, high - low + 1)

    return res
```

To solve this problem, we can use a sliding window approach. The idea is to find the longest subarray in which the
difference between the maximum element and the minimum element (after incrementing any element up to `k` times) is at
most `k`. The frequency of the most frequent element in this subarray will be the maximum frequency we can achieve.

Here's how you can implement this:

1) Sort the Array: First, sort the array. This allows us to use a sliding window to consider subarrays where all
   elements can be made equal by incrementing them.

2) Use a Sliding Window: Iterate through the array using two pointers to maintain a sliding window. The window should
   contain the longest range of numbers that can be made equal with at most `k` increments.

3) Calculate the Required Operations: For each window, calculate the total number of operations needed to make all
   elements in the window equal to the current maximum element.

4) Adjust the Window: If the total operations exceed `k`, move the start of the window forward to reduce the number of
   required operations.

5) Update the Maximum Frequency: The maximum frequency is the size of the current window if the total operations are
   within the allowed limit.