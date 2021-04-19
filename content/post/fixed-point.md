---
title: "Fixed Point"
date: 2021-04-19T22:58:07+03:00
draft: true
categories: ["search"]
---

```kotlin
index == arr[index]
```

[fixed point](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/FixedPoint.kt)

```kotlin
// O(log(n)) time | O(1) space
fun searchFixedPoint(arr: List<Int>): Int {
    var low = 0
    var high = arr.size - 1

    while (low <= high) {
        val mid = low + (high - low) / 2

        when {
            arr[mid] < mid -> low = mid + 1
            arr[mid] == mid && mid == 0 -> return mid
            arr[mid] == mid && arr[mid - 1] < mid - 1 -> return mid
            else -> high = mid - 1
        }
    }

    return -1
}
```
