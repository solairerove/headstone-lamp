---
title: "Find First and Last Position of Element in Sorted Array"
date: 2021-04-19T20:02:54+03:00
draft: true
categories: ["search"]
---

[leetcode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

[search range](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/FindFirstAndLastPositionOfElement.kt)

```kotlin
// O(log(n)) time | O(1) space
fun searchRange(arr: List<Int>, target: Int): Pair<Int, Int> {
    return Pair(findFirstIndex(arr, target), findLastIndex(arr, target))
}

fun findFirstIndex(arr: List<Int>, target: Int): Int {
    var idx = -1
    var low = 0
    var high = arr.size - 1

    while (low <= high) {
        val mid = low + (high - low) / 2

        when {
            arr[mid] >= target -> high = mid - 1
            else -> low = mid + 1
        }

        if (arr[mid] == target) idx = mid
    }

    return idx
}

fun findLastIndex(arr: List<Int>, target: Int): Int {
    var idx = -1
    var low = 0
    var high = arr.size - 1

    while (low <= high) {
        val mid = low + (high - low) / 2

        when {
            arr[mid] <= target -> low = mid + 1
            else -> high = mid - 1
        }

        if (arr[mid] == target) idx = mid
    }

    return idx
}
```
