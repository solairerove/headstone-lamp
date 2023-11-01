---
title: 347. Top K Frequent Elements
description: heapq to obtain the k largest number in O(nlogk) time.
date: 2023-11-01
tags: [ arrays, heap, medium ]
---

Use Python's heapq library to obtain the k largest number in O(nlogk) time.

```python
# O(n * log(k)) time || O(k) space
def find_kth_largest_heap(self, nums: List[int], k: int) -> int:
    return heapq.nlargest(k, nums)[-1]
```
