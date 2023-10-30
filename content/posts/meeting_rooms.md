---
title: 252. Meeting Rooms
description: ensure that no two meetings overlap
date: 2023-10-30
tags: [ arrays, sorting, easy ]
---

```python
# O(n * log(n)) time || O(n) space
def can_attend_meetings(self, intervals: List[List[int]]) -> bool:
    intervals.sort(key=lambda x: x[0])
    for i in range(1, len(intervals)):
        if intervals[i][0] < intervals[i - 1][1]:
            return False

    return True
```

```python
# O(n * log(n)) time || O(n) space
def can_attend_meetings_shorter(self, intervals: List[List[int]]) -> bool:
    intervals.sort(key=lambda x: x[0])

    return all(intervals[i][0] >= intervals[i - 1][1] for i in range(1, len(intervals)))
```

To determine whether a person can attend all meetings, we need to ensure that no two meetings overlap.

A simple approach to solving this problem is:

1) Sort the intervals by their start time.
2) Loop through the sorted list and check if the start time of the current meeting is earlier than the end time of the
   previous meeting. If it is, then the meetings overlap, and the person cannot attend all of them.
