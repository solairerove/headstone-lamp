---
title: 56. Merge Intervals
description: sort the intervals based on their start times, merge the two by updating the end time
date: 2023-10-27
tags: [ arrays, medium ]
---

```python
# O(n * log(n)) time || O(n) space
def merge(self, intervals: List[List[int]]) -> List[List[int]]:
    intervals.sort(key=lambda x: x[0])

    res = [intervals[0]]
    for i in range(1, len(intervals)):
        if intervals[i][0] > res[-1][1]:
            res.append(intervals[i])
        else:
            res[-1][1] = max(res[-1][1], intervals[i][1])

    return res
```

This is a classic interval problem. The idea is to first sort the intervals based on their start times. After sorting,
you can then iterate over the sorted intervals and merge those that overlap. Here's a step-by-step breakdown of the
approach:

1) Sort Intervals: Sort the intervals array based on the start times. This ensures that if two intervals overlap, the
   one
   with the earlier start time comes first.
2) Iterate and Merge: Initialize a result array. For each interval:
    - If the result array is empty or the current interval's start time is greater than the last interval's end time in
      the result array, append the current interval to the result.
    - Otherwise, if there's an overlap (i.e., the current interval's start time is less than or equal to the last
      interval's end time in the result array), merge the two by updating the end time of the last interval in the
      result array.