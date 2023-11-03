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

Quickselect with optimisations.

```python
# O(n) time || O(n) space
def kth_largest_number_quickselect(self, nums: List[str], k: int) -> str:
    return str(quickselect([int(num) for num in nums], 0, len(nums) - 1, len(nums) - k))


def quickselect(arr, low, high, k):
    if low == high:
        return arr[low]

    lt, gt = partition(arr, low, high, random.randint(low, high))
    if k < lt:
        return quickselect(arr, low, lt - 1, k)
    elif k <= gt:
        return arr[k]
    else:
        return quickselect(arr, gt + 1, high, k)


def partition(arr, low, high, idx):
    pivot = arr[idx]
    lt, i, gt = low, low, high
    while i <= gt:
        if arr[i] < pivot:
            arr[i], arr[lt] = arr[lt], arr[i]
            i, lt = i + 1, lt + 1
        elif arr[i] > pivot:
            arr[i], arr[gt] = arr[gt], arr[i]
            gt -= 1
        else:
            i += 1

    return lt, gt
```
