---
title: 347. Top K Frequent Elements
description:
date: 2023-11-01
tags: [ arrays, heap, medium ]
---

- calculate how frequent you can see num in arr
- create frequency array where index is frequency and value is arr of keys
- traverse from end to start and append to res
- don't use this solution during interview

```python
# O(n) time || O(n) space
def top_k_frequent_linear(self, nums: List[int], k: int) -> List[int]:
    if k == len(nums):
        return nums

    cnt = collections.Counter(nums)
    freq = [[] for _ in range(len(nums) + 1)]
    for key, val in cnt.items():
        freq[val].append(key)

    res = []
    for i in range(len(freq) - 1, 0, -1):
        for num in freq[i]:
            res.append(num)

            if len(res) == k:
                return res
```
