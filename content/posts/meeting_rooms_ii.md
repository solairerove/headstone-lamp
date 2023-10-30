---
title: 253. Meeting Rooms II
description: sort both start times and end times, determine at any given time how many rooms are in use.
date: 2023-10-30
tags: [ arrays, sorting, medium ]
---

```python
# O(n * log(n)) time || O(n) space
def min_meeting_rooms(self, intervals: List[List[int]]) -> int:
    start_times = sorted([i[0] for i in intervals])
    end_times = sorted([i[1] for i in intervals])

    res = 0
    start, end = 0, 0
    while start < len(intervals):
        if start_times[start] >= end_times[end]:
            res, end = res - 1, end + 1

        res, start = res + 1, start + 1

    return res
```

To solve this problem, we can think of the start and end times of the intervals as events. For every start time, we need
a new room, and for every end time, a room gets freed up. We'll sort both start times and end times, then we can just
iterate through both lists to determine at any given time how many rooms are in use.

Here's the step-by-step approach:

1) Separate out the start times and end times and sort them individually.
2) Use two pointers to traverse both the start times and the end times.
3) When the current start time is less than the current end time, it means a new meeting has started, and we haven't yet
   finished the previous one, so we need a new room.
4) Move the pointer for the start times forward.
5) If the current start time is greater than or equal to the current end time, it means a meeting has ended by the time
   the current meeting starts. So, we can use the same room for this meeting. Move the pointer for the end times
   forward.
6) Keep track of the number of rooms in use at any given time and update the maximum rooms used.
