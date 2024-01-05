---
title: 300. Longest Increasing Subsequence
description: dp, traverse array, compare current with all previous in range, update dp if current bigger than prev
date: 2024-01-05
tags: [ dp, arrays, medium ]
---

```python
# O(n^2) time || O(n) space
def length_of_lis_bottom_up(self, nums: List[int]) -> int:
    n = len(nums)
    dp = [1] * n
    for i in range(1, n):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)
```

```python
# O(n * log(n)) time || O(n) space
def length_of_lis(self, nums: List[int]) -> int:
    sub = []
    for n in nums:
        i = bisect_left(sub, n)
        if i == len(sub):
            sub.append(n)
        else:
            sub[i] = n

    return len(sub)
```

1) Initialization: Create an array `dp` of the same length as the input array `nums`. Each element in `dp` represents
   the length of the longest increasing subsequence ending at that index. Initialize each element in `dp` with 1,
   because the minimum length of an increasing subsequence is 1 (the number itself).

2) Building the dp Array: Iterate through the `nums` array. For each number `nums[i]`, compare it with all the previous
   numbers `nums[j]` (where `j` < `i`). If `nums[i]` is greater than `nums[j]`, it means you can extend the subsequence
   ending at `j` by adding `nums[i]`. Update dp[i] to be the maximum of its current value and `dp[j] + 1`.

3) Finding the Answer: The length of the longest increasing subsequence will be the maximum value in the dp array after
   you've processed all elements in nums.
