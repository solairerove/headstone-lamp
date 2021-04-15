---
title: "Search in Matrix"
date: 2021-04-15T23:26:27+03:00
draft: true
categories: ["search"]
---

[leetcode](https://leetcode.com/problems/search-a-2d-matrix/)

[third maximum number](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/SearchInMatrix.kt)

```kotlin
// O(n + m) time | O(1) space
fun searchInMatrix(matrix: List<List<Int>>, target: Int): List<Int> {
    var row = 0
    var col = matrix[0].size - 1

    while (row < matrix.size && col >= 0) {
        when {
            matrix[row][col] < target -> row++
            matrix[row][col] > target -> col--
            else -> return listOf(row, col)
        }
    }

    return listOf(-1, -1)
}
```
