---
title: 15. 3Sum
description: sort array, iterate over, avoid duplicates, move borders
date: 2023-10-24
tags: [ arrays, medium ] 
---

```python
# O(n^2) time || O(1) space
def three_sum(self, nums: List[int]) -> List[List[int]]:
    nums.sort()
    res = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        low, high = i + 1, len(nums) - 1
        while low < high:
            _sum = nums[i] + nums[low] + nums[high]

            if _sum == 0:
                res.append([nums[i], nums[low], nums[high]])
                low, high = low + 1, high - 1

                while low < high and nums[low] == nums[low - 1]:
                    low += 1

                while low < high and nums[high] == nums[high + 1]:
                    high -= 1

            elif _sum < 0:
                low += 1
            else:
                high -= 1

    return res
```

You can solve this problem using a sorting-based approach combined with the two-pointer technique. Here's a step-by-step
guide on how to do it:

- Sort the Array: First, sort the array in ascending order. This makes it easier to avoid duplicate triplets and use the
  two-pointer technique.
- Initialize a Result List: Create a list to store the triplets.
- Iterate Through the Array: Loop through the array with a for loop.
- Let’s call the current element `nums[i]`. For each `nums[i]`, you are going to find pairs of numbers in the subarray
  `nums[i+1:]` that add up to `-nums[i]`.
- Two-Pointer Technique: Use two pointers, left and right, initialized at i+1 and len(nums) - 1, respectively. In each
  iteration, check if `nums[i] + nums[left] + nums[right]` is 0.
    - If it is, add `[nums[i], nums[left], nums[right]]` to the result list, and move both pointers towards the center.
    - If the sum is less than 0, move the left pointer to the right.
    - If the sum is greater than 0, move the right pointer to the left.
- Avoid Duplicate Triplets: Ensure that you don’t add duplicate triplets to the result list. You can do this by skipping
  over duplicate values of `nums[i]`, `nums[left]`, and `nums[right]`.
- Return the Result: After the loop, return the result list.
