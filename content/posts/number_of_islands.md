---
title: 200. Number of Islands
description: 
date: 2023-10-26
tags: [ arrays, dfs, medium ]
---

```python
# O(n * m) time || O(n * m) space
def num_islands_dfs(self, grid: List[List[str]]) -> int:
    if not grid:
        return 0

    n, m = len(grid), len(grid[0])

    def dfs(i, j):
        if 0 <= i < n and 0 <= j < m and grid[i][j] == "1":
            grid[i][j] = "0"
            dfs(i - 1, j)
            dfs(i + 1, j)
            dfs(i, j - 1)
            dfs(i, j + 1)
        else:
            return

    res = 0
    for i in range(n):
        for j in range(m):
            if grid[i][j] == "1":
                res += 1
                dfs(i, j)

    return res
```

```python
# O(n * m) time || O(n * m) space
def num_islands_dfs_shorter(self, grid: List[List[str]]) -> int:
    if not grid:
        return 0

    n, m = len(grid), len(grid[0])

    def dfs(i, j):
        if 0 <= i < n and 0 <= j < m and grid[i][j] == "1":
            grid[i][j] = "0"
            list(map(dfs, [i - 1, i + 1, i, i], [j, j, j - 1, j + 1]))

    res = 0
    for i in range(n):
        for j in range(m):
            if grid[i][j] == "1":
                res += 1
                dfs(i, j)

    return res
```

This problem is a classic example where Depth First Search (DFS) can be used. Every time we find a "1", we start a DFS traversal to mark all the connected "1"s. Every island will initiate exactly one DFS traversal. Therefore, by counting how many times DFS is called, we can find out the number of islands.

Here's how the algorithm works:

1) Loop through each cell in the grid.
2) If the cell value is "1", increment our island counter and start a DFS traversal from that cell.
3) Within the DFS traversal, mark the visited cell as "0" (water) to ensure we don't visit it again.
4) Visit the 4 possible directions from the current cell (top, bottom, left, right). If we find a cell with value "1", continue the DFS traversal from that cell.
5) Once we have visited all the cells of an island using DFS, return to the main loop and continue checking the next cell.
