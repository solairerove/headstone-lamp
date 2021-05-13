---
title: "First Duplicate Value"
date: 2021-05-13T12:40:48+03:00
draft: true
categories: ["arrays"]
---

Input:  [2, 3, 2, 6, 6, 5, 3, 6] \
Output: 2

Naive O(n) time | O(n) space solution is to use set and contains check 

[first duplicate value](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/FirstDuplicateValue.kt)

```kotlin
// O(n) time | O(1) space
fun firstDuplicateValue(arr: MutableList<Int>): Int {
    for (el in arr) {
        val absEl = abs(el)
        if (arr[absEl - 1] < 0) return absEl
        arr[absEl - 1] *= -1
    }

    return -1
}
```
