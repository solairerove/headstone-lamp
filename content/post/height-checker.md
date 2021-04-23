---
title: "Height Checker"
date: 2021-04-23T17:49:34+03:00
draft: true
categories: ["greedy"]
---

Input: red = [1, 5, 9, 4, 6], blue = [4, 8, 6, 5, 3] \
Output: false

[height checker](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/HeightChecker.kt) \
type of [leet code](https://leetcode.com/problems/height-checker/)

```kotlin
// O(nlog(n)) time | O(1) space
fun heightChecker(red: MutableList<Int>, blue: MutableList<Int>): Boolean {
    red.sortDescending()
    blue.sortDescending()

    val firstRow = if (red[0] < blue[0]) 1 else 0

    for (i in 0 until red.size) {
        val r = red[i]
        val b = blue[i]

        if (firstRow == 1) {
            if (r >= b) return false
        } else {
            if (r <= b) return false
        }
    }

    return true
}
```
