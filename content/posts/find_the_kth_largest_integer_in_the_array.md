---
title: 1985. Find the Kth Largest Integer in the Array
description: heapq library to obtain the kth largest number in O(n * log(k * m)) time.
date: 2023-11-02
tags: [ arrays, heap, medium ]
---

Use Python's heapq library to obtain the kth largest number in O(n * log(k * m)) time.

```python
# O(n * log(k * m)) time || O(k) space
# n is len of nums
# m is len of each num
# k is k
def kth_largest_number_heap(self, nums: List[str], k: int) -> str:
    heap = []
    for num in nums:
        heapq.heappush(heap, int(num))
        if len(heap) > k:
            heapq.heappop(heap)

    return str(heap[0])
```
