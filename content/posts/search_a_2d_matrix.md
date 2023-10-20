---
title: 74. Search a 2D Matrix
description: use binary search to find and imagine matrix as sorted array
date: 2023-10-20
tags: [ binary-search, medium ] 
---

```python
# O(log(m * n)) time || O(1) space
def search_matrix(self, matrix: List[List[int]], target: int) -> bool:
    rows, cols = len(matrix), len(matrix[0])
    low, high = 0, rows * cols - 1
    while low <= high:
        mid = low + (high - low) // 2
        mid_row, mid_col = divmod(mid, cols)

        if target == matrix[mid_row][mid_col]:
            return True
        elif target < matrix[mid_row][mid_col]:
            high = mid - 1
        else:
            low = mid + 1

    return False
```

to get midpoint in the matrix, we use the `divmod` function with `mid` and `cols`
