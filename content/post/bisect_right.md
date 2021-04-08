---
title: "Bisect right"
date: 2021-04-08T22:24:43+03:00
draft: true
categories: ["search"]
---

[binary select right](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/BiSectRight.kt)

```kotlin
// O(log(n)) time | O(1) space
fun biSectRight(arr: List<Int>, target: Int, lo: Int = 0, hi: Int = arr.size): Int {
    val n = arr.size
    if (n == 0) return 0

    var low = lo
    var high = hi

    if (target < arr[low]) return low
    if (target > arr[high - 1]) return high

    while (true) {
        if (low + 1 == high) {
            return low + 1
        }

        val mid = low + (high - low) / 2

        when {
            target < arr[mid] -> high = mid
            else -> low = mid
        }
    }
}

```
