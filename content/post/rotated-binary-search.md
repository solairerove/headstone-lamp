---
title: "Rotated Binary Search"
date: 2021-04-16T23:51:48+03:00
draft: true
categories: ["search"]
---

[leetcode](https://leetcode.com/problems/search-in-rotated-sorted-array/)

[rotated binary search](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/RotatedBinarySearch.kt)

```kotlin
// O(log(n)) time | O(1) space
fun rotatedBinarySearch(arr: List<Int>, k: Int): Int {
    var low = 0
    var high = arr.size - 1

    while (low <= high) {
        val mid = low + (high - low) / 2

        if (arr[mid] == k) return mid
        else if (arr[low] <= k) {
            if (k < arr[mid] && k >= arr[low]) high = mid - 1
            else low = mid + 1
        } else {
            if (k > arr[mid] && k <= arr[high]) low = mid + 1
            else high = mid - 1
        }
    }

    return -1
}
```
