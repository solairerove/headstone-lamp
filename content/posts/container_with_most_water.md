---
title: 11. Container With Most Water
description: medium
date: 2023-03-20
tags: [two-pointers, arrays] 
---

```python
# O(n) time || O(1) space
def max_area(self, height: List[int]) -> int:
    area, low, high = 0, 0, len(height) - 1
    while low < high:
        area = max(area, min(height[low], height[high]) * (high - low))
        if height[low] <= height[high]:
            low += 1
        else:
            high -= 1

    return area
```
