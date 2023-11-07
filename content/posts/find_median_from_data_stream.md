---
title: 295. Find Median from Data Stream
description:
date: 2023-11-07
tags: [ heap, hard ] 
---

```python
from heapq import heappush, heappop


class MedianFinder:

    # O(1) time || O(n) space
    def __init__(self):
        self.small = []  # [0] is highest among small numbers, max heap
        self.large = []  # [0] is lowest among large numbers, min heap

    # O(log(n)) time || O(n) space
    def add_num(self, num: int) -> None:
        if not self.small or num <= -self.small[0]:
            heappush(self.small, -num)
        else:
            heappush(self.large, num)

        if len(self.small) > len(self.large) + 1:
            heappush(self.large, -heappop(self.small))

        if len(self.small) < len(self.large):
            heappush(self.small, -heappop(self.large))

    # O(1) time || O(1) space
    def find_median(self) -> float:
        if len(self.small) > len(self.large):
            return -self.small[0]

        return (-self.small[0] + self.large[0]) / 2
```

This problem can be solved efficiently by using two priority queues (heaps) in Python: a max heap to store the lower
half of the numbers and a min heap to store the upper half. The max heap allows us to quickly access the largest number
in the lower half, while the min heap gives us quick access to the smallest number in the upper half.

The key to this approach is to balance the two heaps so that:

- If the total number of elements is odd, the max heap contains one more element than the min heap.
- If the total number of elements is even, both heaps contain the same number of elements.

When these conditions are met, the median can be found by either taking the top element from the max heap (if the
total number of elements is odd) or by averaging the top elements of both heaps (if the total number of elements is
even).