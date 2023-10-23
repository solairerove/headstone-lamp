---
title: 136. Single Number
description: perform the XOR operation with unique, this will "cancel out" the duplicates
date: 2023-10-23
tags: [ array, math, bit-manipulation, easy ] 
---

```python
# O(n) time || O(1) space
def single_number(self, nums: List[int]) -> int:
    res = 0
    for n in nums:
        res ^= n

    return res
```

```python
# O(n) time || O(1) space
def single_number_reduce(self, nums: List[int]) -> int:
    return functools.reduce(lambda x, y: x ^ y, nums)
```

To find the element that appears only once in the array with a linear runtime complexity and constant extra space, \
you can utilize the XOR operator.

Here's the algorithm to solve the problem:

    Initialize a variable unique to 0.

    Iterate through each element in the array nums.

    For each element, perform the XOR operation with unique. This will "cancel out" the duplicates.

    After iterating through all the elements, the value of unique will be the element that appears only once.

    Return the value of unique.
