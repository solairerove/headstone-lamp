---
title: 374. Guess Number Higher or Lower
description: it's pretty much the same as 278. First Bad Version
date: 2023-10-20
tags: [ binary-search, easy ] 
---

```python
# @param num, your guess
# @return -1 if num is higher than the picked number
#          1 if num is lower than the picked number
#          otherwise return 0
# def guess(num: int) -> int:

# O(log(n)) time || O(1) space
def guess_number(self, n: int) -> int:
    low, high = 1, n
    while low <= high:
        mid = low + (high - low) // 2
        cmp = guess(mid)
        if cmp == 0:
            return mid
        elif cmp == -1:
            high = mid - 1
        else:
            low = mid + 1
```

you can use binary search to decrease count of api calls. \
if pick number (target) lower than your number, in other words guess return `-1`, cut `high` border.
