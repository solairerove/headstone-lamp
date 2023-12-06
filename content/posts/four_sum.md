---
title: 18. 4Sum
description: fix the first two numbers using nested loops find the other two numbers using the two-pointer approach
date: 2023-10-24
tags: [ arrays, medium ] 
---

```python
# O(n^3) time || O(1) space
def four_sum(self, nums: List[int], target: int) -> List[List[int]]:
    nums.sort()
    res = []
    for i in range(len(nums) - 3):
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        for j in range(i + 1, len(nums) - 2):
            if j > i + 1 and nums[j] == nums[j - 1]:
                continue

            low, high = j + 1, len(nums) - 1
            while low < high:
                _sum = nums[i] + nums[j] + nums[low] + nums[high]

                if _sum == target:
                    res.append([nums[i], nums[j], nums[low], nums[high]])
                    low, high = low + 1, high - 1

                    while low < high and nums[low] == nums[low - 1]:
                        low += 1

                    while low < high and nums[high] == nums[high + 1]:
                        high -= 1

                elif _sum < target:
                    low += 1
                else:
                    high -= 1

    return res
```

To solve this problem, you can use a similar approach to the one used for the 3Sum problem but with an additional layer
of nested loops. Here's a general approach:

- Sort the array: This helps in skipping over duplicate values and in using the two-pointer technique.
- Nested loops: Use two nested loops to fix two numbers, and then use the two-pointer technique to find the remaining
  two numbers.
- Avoid duplicates: Skip over duplicate values to avoid adding duplicate quadruplets.
- Two-pointer technique: For the remaining two numbers, use two pointers,
    - one starting from the next of the second loop and the other from the end of the array.
- Move the pointers based on the sum comparison with the target.

Wrapping Up
After the while loop, we return to our nested for loops and try the next pair of `i` and `j`. Once all loops are complete,
we return the result.

In summary, the core idea is to fix the first two numbers using nested loops and then find the other two numbers using
the two-pointer approach. The conditions inside the loops ensure we don't get duplicate quadruplets.
