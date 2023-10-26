---
title: 875. Koko Eating Bananas
description: if current speed is ok, the result will be on it's left inclusively
date: 2023-10-23
tags: [ binary-search, medium ] 
---

```python
# O(n * log(max(p)) time || O(1) space
def min_eating_speed(self, piles: List[int], h: int) -> int:
    low, high = 1, max(piles)
    while low < high:
        mid = low + (high - low) // 2
        if sum(math.ceil(pile / mid) for pile in piles) <= h:
            high = mid
        else:
            low = mid + 1

    return high
```

if the current speed is workable, the minimum workable speed should be on its left inclusively. if the current speed is
not workable, that is, too slow to finish the eating task, then the minimum workable speed should be on its right
exclusively.

therefore, we can use binary search to locate the boundary that separates workable speeds and unworkable speeds, to get
the minimum workable speed.

find current speed by traversing piles, adjust border depends on speed.
