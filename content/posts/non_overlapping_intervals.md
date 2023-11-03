---
title: 435. Non-overlapping Intervals
description: sort the intervals based on their end times, check for next start and last end overlap
date: 2023-10-30
tags: [ arrays, sorting, greedy, medium ]
---

```python
# O(n * log(n)) time || O(log(n)) space
def erase_overlap_intervals(self, intervals: List[List[int]]) -> int:
    intervals.sort(key=lambda x: x[1])

    res = 0
    end = intervals[0][1]
    for interval in intervals[1:]:
        if interval[0] < end:
            res += 1
        else:
            end = interval[1]

    return res
```

To solve this problem, we can take a greedy approach. The intuition is that if we choose intervals that end early, it
gives us more room for subsequent intervals to fit without overlapping.

### Approach:

1) Sort the intervals based on their end times. This ensures that we are considering intervals in the order they end. By
   doing this, we are maximizing the space for subsequent intervals.
2) Initialize two variables:
   end to keep track of the end time of the last selected interval (initialized to negative infinity since we haven't
   selected any interval yet).
   count to count the number of intervals to remove (initialized to 0).
3) Iterate through the sorted intervals:
   For each interval, if its start time is greater than or equal to the end time of the last selected interval, it means
   this interval doesn't overlap with the previously selected interval. So, update end to be the end time of the current
   interval.
   If the interval's start time is less than the end time of the last selected interval, it overlaps with the selected
   interval. Increment the count.
4) Return count.

The term "greedy approach" in algorithms refers to the strategy of making the most optimal choice at each step with the
hopes of finding a global optimum. Instead of looking at all the possible solutions (which can be very vast) and then
deciding the best one, a greedy algorithm chooses the best option at every single step.

In the context of the overlapping intervals problem, the greedy approach is evident in the way we make local decisions:

1) In the approach (sorting by end times):
   By choosing intervals that end earlier, we are greedily trying to free up time for subsequent intervals. The logic
   is, the earlier an interval ends, the more space there is for later intervals to fit in without overlapping. We are
   not looking ahead to see if this choice affects future intervals; we are simply making the best decision based on the
   current set of circumstances.
