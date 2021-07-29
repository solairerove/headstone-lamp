---
title: "Number of Islands"
date: 2021-07-29T16:28:46+03:00
draft: true
categories: ["arrays"]
---

Input:
```
[1 1 0 0 0] 
[1 1 0 0 0] 
[0 0 1 0 0] 
[0 0 0 1 1]
```
Output: 3

[number of islands](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/NumberOfIslands.kt)
[leetcode](https://leetcode.com/problems/number-of-islands/)

```kotlin
// O(m * n) time | O(m * n) space
fun numIslandsDFS(grid: List<MutableList<String>>): Int {
    if (grid.isEmpty()) return 0

    val row = grid.size
    val col = grid[0].size
    var count = 0
    for (r in 0 until row) {
        for (c in 0 until col) {
            if (grid[r][c] == "1") {
                count++
                dsf(grid, r, c)
            }
        }
    }

    return count
}

fun dsf(grid: List<MutableList<String>>, r: Int, c: Int) {
    val row = grid.size
    val col = grid[0].size

    if (r < 0 || c < 0 || r >= row || c >= col || grid[r][c] == "0") return

    grid[r][c] = "0"
    dsf(grid, r - 1, c)
    dsf(grid, r + 1, c)
    dsf(grid, r, c - 1)
    dsf(grid, r, c + 1)
}
```
