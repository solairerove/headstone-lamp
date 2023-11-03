---
title: 215. Kth Largest Element in an Array
description: heapq to obtain the k largest number in O(nlogk) time.
date: 2023-11-02
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
