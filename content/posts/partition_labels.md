---
title: 763. Partition Labels
description: use two-pointer technique, calculate Area = width * height
date: 2023-11-06
tags: [ two-pointers, arrays, medium ] 
---

```python
# O(n) time || O(1) space
def partition_labels(self, s: str) -> List[int]:
    last_occurrence = {c: i for i, c in enumerate(s)}
    res = []
    low = high = 0
    for i, c in enumerate(s):
        high = max(high, last_occurrence[c])

        if i == high:
            res.append(high - low + 1)
            low = high + 1

    return res
```

This problem, often referred to as "Partition Labels" on LeetCode, requires us to split the string into the maximum
number of parts such that no letter appears in more than one part. The solution involves a greedy approach, and here is
the intuition behind it:

1) **Record Last Occurrences**: First, we need to record the last position of each character in the string because a
   character cannot be in two parts and must be in the same part as its last occurrence.

2) **Iterate and Partition**: Then, we iterate through the string while keeping track of the 'farthest' index we need to
   consider for the current partition (which is the farthest last occurrence of any character encountered so far in the
   current part). If we reach a point where the current index is the same as the 'farthest' index, we can end the
   partition at this point.

Explanation for Example 1:

- We start with the letter 'a' which last appears at index 8. So, our initial end is 8.
- As we go on, we see that 'b' and 'c' also have their last occurrences within this range (indices 5 and 7
  respectively).
- When we reach index 8, we haven't encountered any character that has a last occurrence beyond 8, so we can make a cut
  here. The size of this part is 9 (`end - start + 1`).
- We then repeat the process for the remaining string.

Explanation for Example 2:

- The letter 'c' last occurs at index 9, 'b' at index 8, and 'd' at index 7, 'e' at index 5.
- All the characters of the string are within the first encountered last occurrence index of 'c', so the whole string is
  one part, and its length is 10.

The time complexity of this algorithm is O(n), where n is the length of the string, because we make one pass to find the
last occurrences, and one pass to determine the partitions. The space complexity is O(1) because the size of the
`last_occurrence` dictionary is bounded by the size of the alphabet, which is constant for this problem.