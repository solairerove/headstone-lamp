---
title: "Powerset"
date: 2021-06-07T19:42:59+03:00
draft: true
categories: ["recursion"]
---

Input: [1, 2] \
Output: [[], [1], [2], [1, 2]]

[powerset](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/recursion/Powerset.kt)

```kotlin
// O(n*2ˆn) time | O(n*2ˆn) space
fun powerset(arr: List<Int>): List<List<Int>> {
    val sets = mutableListOf(listOf<Int>())
    for (el in arr) {
        for (i in 0 until sets.size) {
            val curr = sets[i].toMutableList()
            curr.add(el)
            sets.add(curr)
        }
    }
    return sets
}
```
