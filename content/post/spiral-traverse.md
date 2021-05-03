---
title: "Spiral Traverse"
date: 2021-05-03T20:43:19+03:00
draft: true
categories: ["arrays"]
---

Input: arr = [[8, 2, -2, -4, 1], [3, 5, 10, 6, 4], [4, 10, -2, 1, 9], [6, 9, -4, 0, -1]] \
Output: [8, 2, -2, -4, 1, 4, 9, -1, 0, -4, 9, 6, 4, 3, 5, 10, 6, 1, -2, 10]

[spiral traverse](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/SpiralTraverse.kt)

```kotlin
// O(n) time | O(n) space
fun spiralTraverse(arr: List<List<Int>>): List<Int> {
    val res = mutableListOf<Int>()
    var lowRow = 0
    var highRow = arr.size - 1
    var lowCol = 0
    var highCol = arr[0].size - 1

    while (lowRow <= highRow && lowCol <= highCol) {
        for (col in lowCol..highCol) {
            res.add(arr[lowRow][col])
        }

        for (row in lowRow + 1..highRow) {
            res.add(arr[row][highCol])
        }

        for (col in highCol - 1 downTo lowCol) {
            if (lowRow == highRow) break
            res.add(arr[highRow][col])
        }

        for (row in highRow - 1 downTo lowRow + 1) {
            if (lowCol == highCol) break
            res.add(arr[row][lowCol])
        }

        lowRow++
        highRow--
        lowCol++
        highCol--
    }

    return res
}
```
