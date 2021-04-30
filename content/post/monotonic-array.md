---
title: "Monotonic Array"
date: 2021-04-30T16:16:13+03:00
draft: true
categories: ["arrays"]
---

Input: arr = [-10, -9, -4, 0, 1, 2, 3, 5, 9, 11, 12, 14, 17] \
Output: true

[monotonic array](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/MonotonicArray.kt)

```kotlin
// O(n) time | O(1) space
fun isMonotonic(arr: List<Int>): Boolean {
    var isIncreasing = true
    var isDecreasing = true

    for (i in 1 until arr.size) {
        when {
            arr[i - 1] < arr[i] -> isDecreasing = false
            arr[i - 1] > arr[i] -> isIncreasing = false
        }
    }

    return isIncreasing || isDecreasing
}
```
