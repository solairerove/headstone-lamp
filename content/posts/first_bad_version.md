---
title: 278. First Bad Version
description: use binary search to find low border of bad version
date: 2023-10-20
tags: [ binary-search, easy ] 
---

```python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

# O(log(n)) time || O(1) space
def first_bad_version(self, n: int) -> int:
    low, high = 1, n
    while low <= high:
        mid = low + (high - low) // 2
        if isBadVersion(mid):
            high = mid - 1
        else:
            low = mid + 1

    return low
```

you can use binary search to decrease count of api calls. \
if `ith` bad version is false, decrease `high` border, if true then increase `low`. \
`low` is first bad version, you're free to return it
