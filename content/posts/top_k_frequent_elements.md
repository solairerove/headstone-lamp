---
title: 347. Top K Frequent Elements
description:
date: 2023-11-01
tags: [ arrays, heap, medium ]
---

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
