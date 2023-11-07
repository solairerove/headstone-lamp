---
title: 239. Sliding Window Maximum
description: maintain a deque of candidates idx in decreasing order only from the current sliding window
date: 2023-11-07
tags: [ sliding-window, array, hard ] 
---

```python
# O(n) time | O(k) space
def max_sliding_window(self, nums: List[int], k: int) -> List[int]:
    dq = collections.deque()
    res = []
    for i, n in enumerate(nums):
        if dq and dq[0] < i - k + 1:
            dq.popleft()

        while dq and nums[dq[-1]] <= n:
            dq.pop()

        dq.append(i)

        if i >= k - 1:
            res.append(nums[dq[0]])

    return res
```

This is a classic sliding window problem that can be efficiently solved using a deque (double-ended queue). The idea is
to maintain a deque of candidates in decreasing order and to ensure that the candidates are only from the current
sliding window.

Here's the step-by-step strategy:

1) Initialize a deque `D` to store indices of array elements. The deque will store indices in decreasing order of their
   corresponding array values.

2) Iterate over the array:
    - Clean the deque:
        - Remove indices of elements not from the sliding window (i.e., `i - k >= D.front()`).
        - Remove indices of all elements smaller than the current element since they will not be needed (i.e.,
          `nums[i] >= nums[D.back()]`).
    - Add the current element index to the deque.
    - If the window has reached size `k`, append the current max to the output, which is the element corresponding to
      `D.front()`.