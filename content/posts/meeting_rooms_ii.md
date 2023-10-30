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

```python
# O(n * log(n)) time || O(n) space
def min_meeting_rooms_heap(self, intervals: List[List[int]]) -> int:
    intervals.sort(key=lambda x: x[0])

    heap = []
    heapq.heappush(heap, intervals[0][1])
    for interval in intervals[1:]:
        if interval[0] >= heap[0]:
            heapq.heappop(heap)

        heapq.heappush(heap, interval[1])

    return len(heap)
```

### Intuition:

The fundamental idea behind the heap-based solution is to keep track of the end times of meetings in rooms. If a new
meeting starts after the earliest meeting (the one at the top of the heap) ends, we can reuse that room; otherwise, we
need a new room.

### Detailed Steps:

1) Sort by Start Time:
    - We first sort the intervals based on their start times. This ensures that as we iterate through the intervals, we
      are considering meetings in the order they start.
2) Initialize a Min-Heap:
    - We use a min-heap to keep track of the end times of meetings. The meeting that ends the earliest will always be at
      the top of the heap.
3) Iterate Through Meetings:
    - For the first meeting, we don't have a choice but to allocate a new room. So, we add the end time of the first
      meeting to the heap.
    - For every subsequent meeting:
        - We compare its start time with the minimum end time (i.e., the end time at the top of the heap).
        - If the start time of the current meeting is greater than or equal to the minimum end time, it means the room
          has been freed and can be reused. In this case, we pop the top element from the heap (to "free" the room) and
          push the current meeting's end time (to represent the room being occupied till the end of the current
          meeting).
        - If the start time of the current meeting is less than the minimum end time, we need a new room. So, we just
          add the current meeting's end time to the heap.
4) Result:

- The size of the heap will tell us the total number of rooms booked at any point in time, which is our answer.