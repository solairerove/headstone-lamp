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

Quickselect with optimisations. Works very slow on leetcode cases. Maybe median of medians will help.

```python
# O(max(n, n^2) time || O(1) space
def find_kth_largest_quickselect(self, nums: List[int], k: int) -> int:
    return quickselect(nums, 0, len(nums) - 1, len(nums) - k)  # nums[len(nums) - k]


def quickselect(arr, low, high, k):
    if low == high:
        return arr[low]

    pivot_idx = random.randint(low, high)
    lt, gt = partition(arr, low, high, pivot_idx)
    if k < lt:
        return quickselect(arr, low, lt - 1, k)
    elif k <= gt:
        return arr[k]
    else:
        return quickselect(arr, gt + 1, high, k)


def partition(arr, low, high, pivot_idx):
    pivot = arr[pivot_idx]
    lt, i, gt = low, low, high
    while i <= gt:
        if arr[i] < pivot:
            arr[lt], arr[i] = arr[i], arr[lt]
            lt, i = lt + 1, i + 1
        elif arr[i] > pivot:
            arr[gt], arr[i] = arr[i], arr[gt]
            gt -= 1
        else:
            i += 1

    return lt, gt
```
