---
title: "Sort Squared Array"
date: 2021-05-05T13:43:52+03:00
draft: true
categories: ["arrays"]
---

Input: arr = [-2, -1, 3, 4, 6, 7, 9, 10] \
Output: [1, 4, 9, 16, 36, 49, 81, 100]

[sorted squared array](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/SortedSquaredArray.kt)

```kotlin
// O(n) time | O(n) space
fun sortedSquaredArray(arr: List<Int>): List<Int> {
    val n = arr.size

    val sortedSquared = MutableList(n) { 0 }
    var low = 0
    var high = n - 1

    for (i in n - 1 downTo 0) {
        val lowEl = arr[low]
        val highEl = arr[high]

        if (abs(highEl) > abs(lowEl)) {
            sortedSquared[i] = highEl * highEl
            high--
        } else {
            sortedSquared[i] = lowEl * lowEl
            low++
        }
    }

    return sortedSquared
}
```
