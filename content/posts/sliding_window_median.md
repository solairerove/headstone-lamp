---
title: 480. Sliding Window Median
description: steroid version of 295 Median Finder with lazy removals and balance variable
date: 2023-11-10
tags: [ sliding-window, heap, hard ] 
---

```python
class MedianFinder:
    def __init__(self):
        self.small, self.large = [], []
        self.lazy = collections.defaultdict(int)
        self.balance = 0

    def add(self, num):
        if not self.small or num <= -self.small[0]:
            heapq.heappush(self.small, -num)
            self.balance -= 1
        else:
            heapq.heappush(self.large, num)
            self.balance += 1

        self.rebalance()

    def remove(self, num):
        self.lazy[num] += 1
        if num <= -self.small[0]:
            self.balance += 1
        else:
            self.balance -= 1

        self.rebalance()
        self.lazy_remove()

    def find_median(self):
        if self.balance == 0:
            return (-self.small[0] + self.large[0]) / 2
        elif self.balance < 0:
            return -self.small[0]
        else:
            return self.large[0]

    def rebalance(self):
        while self.balance < 0:
            heapq.heappush(self.large, -heapq.heappop(self.small))
            self.balance += 2

        while self.balance > 0:
            heapq.heappush(self.small, -heapq.heappop(self.large))
            self.balance -= 2

    def lazy_remove(self):
        while self.small and self.lazy[-self.small[0]] > 0:
            self.lazy[-self.small[0]] -= 1
            heapq.heappop(self.small)

        while self.large and self.lazy[self.large[0]] > 0:
            self.lazy[self.large[0]] -= 1
            heapq.heappop(self.large)


# O(n * log(k)) time || O(n) space
def median_sliding_window(self, nums: List[int], k: int) -> List[float]:
    res = []
    median_finder = MedianFinder()
    for i, num in enumerate(nums):
        median_finder.add(num)

        if i >= k:
            median_finder.remove(nums[i - k])

        if i >= k - 1:
            res.append(median_finder.find_median())

    return res
```

The `MedianFinder` class from `295` is designed to find the median in a dynamic stream of data. It uses two heaps:

1) `small`: a max heap that stores the smaller half of the numbers.
2) `large`: a min heap that stores the larger half of the numbers.

The class maintains a balance variable, which indicates the size difference between the two heaps. A negative balance
indicates that the `small` heap has more elements, while a positive balance indicates that the `large` heap has more.

### Key Methods:

- `add`: Adds a new number to one of the heaps. If the number is less than or equal to the largest number in the small
  heap, it goes into the small heap, otherwise into the large heap. After adding a number, the rebalance_heaps method is
  called to ensure that the heaps remain balanced.
- `remove`: Marks a number for lazy removal by incrementing its count in the lazy_remove dictionary. It adjusts the
  balance based on the value being removed. After marking for removal, it calls rebalance_heaps and
  lazy_remove_from_heaps to ensure the heaps are balanced and to remove the top elements of the heaps if they are marked
  for lazy removal.
- `find_median`: Returns the median based on the balance of the heaps. If the balance is zero, it means the heaps are
  equal in size and the median is the average of the two top elements. If the balance is negative or positive, it
  returns the top element of the small or large heap, respectively.
- `rebalance`: Ensures that the difference in size between the small and large heaps is no more than one. It moves
  elements between the heaps to maintain this balance.
- `lazy_remove`: Removes the elements that are at the top of either heap if they have been marked for lazy removal.
