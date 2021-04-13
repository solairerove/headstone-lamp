---
title: "Quick Select"
date: 2021-04-13T22:01:11+03:00
draft: true
categories: ["search"]
---

[quick select](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/QuickSelect.kt)

```kotlin
// O(n) time | O(1) space
fun quickSelect(arr: MutableList<Int>, k: Int): Int {
    var low = 0
    var high = arr.size - 1

    while (low < high) {
        val j = partition(arr, low, high)

        when {
            j < k -> low = j + 1
            j > k -> high = j - 1
            else -> return arr[j]
        }
    }

    return arr[low]
}

fun partition(arr: MutableList<Int>, low: Int, high: Int): Int {
    var i = low
    var j = high + 1
    val v = arr[low]

    while (true) {
        while (arr[++i] < v) if (i == high) break
        while (v < arr[--j]) if (j == low) break
        if (j <= i) break
        swap(arr, i, j)
    }

    swap(arr, low, j)
    return j
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}
```
