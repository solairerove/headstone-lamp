---
title: 1. Two Sum
description: as we iterate through the array, we check if the complement (target - num) in map
date: 2023-10-23
tags: [ arrays, easy ] 
---

```python
# O(n) time || O(n) space
def two_sum(self, nums: List[int], target: int) -> List[int]:
    dic = collections.defaultdict(int)
    for i, num in enumerate(nums):
        if target - num in dic:
            return [i, dic[target - num]]

        dic[num] = i
```

In this solution, we use a dictionary `dic` to store the numbers encountered so far along with their indices. \
As we iterate through the array, we check if the complement `(target - num)` exists in the num_map dictionary. \
If it does, we return the indices of the two numbers. \
Otherwise, we add the current number and its index to the dictionary.
