---
title: 347. Top K Frequent Elements
description:
date: 2023-11-01
tags: [ arrays, heap, medium ]
---

### Quickselect Explained:

Quickselect is a cousin of the quicksort algorithm. The idea behind quickselect is to find the k-th smallest (or
largest) element without having to sort the entire list.

#### Steps of Quickselect:

1) Choose a 'pivot' element from the list and partition the other elements into two sub-arrays, according to whether
   they are less than or greater than the pivot.
2) Reorder the list so that all elements less than the pivot come before (in no particular order) and all elements
   greater than the pivot come after it (also in no particular order).
3) The 'pivot' is now in its final sorted position.
4) Compare the k-th index with the index of the pivot:
    - If they are the same, we found our k-th element.
    - If the k-th index is less than the pivot index, repeat the process with the left sub-array.
    - If the k-th index is greater than the pivot index, repeat the process with the right sub-array.

### Application to the Problem:

1) Create a frequency dictionary for the numbers.
2) Convert the dictionary into a list of pairs.
3) Use quickselect to find the k-th most frequent pair.
4) Return numbers with frequencies that are greater than or equal to the k-th pair's frequency.

```python
# O(n) time || O(n) space
def top_k_frequent_quickselect(self, nums: List[int], k: int) -> List[int]:
    def partition(arr, low, high):
        pivot = arr[high][1]
        i = low
        for j in range(low, high):
            if arr[j][1] > pivot:
                arr[i], arr[j] = arr[j], arr[i]
                i += 1

        arr[i], arr[high] = arr[high], arr[i]

        return i

    def quickselect(arr, low, high):
        if low == high:
            return arr[low]

        i = partition(arr, low, high)
        if k == i:
            return arr[k]
        elif k < i:
            return quickselect(arr, low, i - 1)
        else:
            return quickselect(arr, i + 1, high)

    unique = list(collections.Counter(nums).items())  # (number, frequency) pairs list
    quickselect(unique, 0, len(unique) - 1)

    return [pair[0] for pair in unique[:k]]
```

Use a bucket sort-like approach which has an average case time complexity of O(n), where n is the length of the nums
list. The idea is to:

1) Use a frequency dictionary to count the occurrence of each number.
2) Create a list of buckets where the index of each bucket corresponds to the frequency of the elements. For instance,
   buckets[3] will contain all elements that appear three times in nums.
3) Iterate through the buckets in reverse (from high frequency to low) to get the top k frequent numbers.

```python
# O(n) time || O(n) space
def top_k_frequent_linear(self, nums: List[int], k: int) -> List[int]:
    if len(nums) == k:
        return nums

    cnt = collections.Counter(nums)
    buckets = [[] for _ in range(len(nums) + 1)]
    for num, freq in cnt.items():
        buckets[freq].append(num)

    res = []
    for i in range(len(nums), 0, -1):
        for num in buckets[i]:
            res.append(num)

            if len(res) == k:
                return res
```

Use Python's heapq library to obtain the top k frequent numbers in O(nlogk) time.

```python
# O(n * log(k)) time || O(n + k) space
def top_k_frequent_heap(self, nums: List[int], k: int) -> List[int]:
    if len(nums) == k:
        return nums

    cnt = collections.Counter(nums)

    return heapq.nlargest(k, cnt.keys(), key=cnt.get)
```
