---
title: "Pivot Index"
date: 2021-04-20T20:20:36+03:00
draft: true
categories: ["arrays"]
---

[leetcode](https://leetcode.com/problems/find-pivot-index/)

[pivot index](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/PivotIndex.kt)

```kotlin
// O(n) time | O(1) space
fun pivotIndex(arr: List<Int>): Int {
    val total = arr.sum()
    var sum = 0

    for (i in arr.indices) {
        if (sum * 2 == total - arr[i]) return i
        sum += arr[i]
    }
    return -1
}
```
