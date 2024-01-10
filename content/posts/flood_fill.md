---
title: 733. Flood Fill
description: use dfs as in number of islands
date: 2024-01-10
tags: [ arrays, dfs-bfs, easy ]
---

```python
# O(n) time || O(n) space
def flood_fill(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:
    rows, cols = len(image), len(image[0])
    original_color = image[sr][sc]
    if original_color == color:
        return image

    def dfs(r, c):
        if 0 <= r < rows and 0 <= c < cols and image[r][c] == original_color:
            image[r][c] = color
            dfs(r - 1, c)
            dfs(r + 1, c)
            dfs(r, c - 1)
            dfs(r, c + 1)

    dfs(sr, sc)

    return image
```

1) Get the original color of the pixel at `(sr, sc)`.
2) Check for boundary conditions: If the starting pixel already has the target color, we don't need to do anything.
3) Recursive Flood Fill: Create a recursive function that:
    - Changes the color of the current pixel.
    - Recursively calls itself for the four adjacent pixels (up, down, left, right) if they are within bounds and have
      the original color.
4) Invoke the recursive function starting from `(sr, sc)`.
