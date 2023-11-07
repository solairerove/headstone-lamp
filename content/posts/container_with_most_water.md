---
title: 11. Container With Most Water
description: use two-pointer technique, calculate Area = width * height
date: 2023-03-20
tags: [ two-pointers, arrays, medium ] 
---

```python
# O(n) time || O(1) space
def max_area(self, height: List[int]) -> int:
   res, low, high = 0, 0, len(height) - 1
   while low < high:
      res = max(res, (high - low) * (min(height[low], height[high])))
      if height[low] <= height[high]:
         low += 1
      else:
         high -= 1

   return res
```

This problem is known as the "Container With Most Water" and is a well-known example of a two-pointer technique.

Here's the strategy to solve it:

1) Initialize two pointers, one at the beginning of the array (`left`) and one at the end (`right`).
2) Calculate the area formed between the lines at the `left` and `right` pointers, and update the maximum area found so far.
3) Move the pointer that points to the shorter line inwards, because if we move the pointer at the taller line, we are
   sure that the area cannot increase - the width is decreasing, and the height is limited by the shorter line.
4) Repeat steps 2 and 3 until the two pointers meet.
   The formula to calculate the area between two lines is:
   `Area = width * height`
   where width is the difference between the indices of the two lines and height is the minimum of the two line heights.
