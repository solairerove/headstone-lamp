---
title: "Move Element to the End"
date: 2021-04-30T16:06:24+03:00
draft: true
categories: ["arrays"]
---

Input: arr = [-9, -7, 2, -4, 0, 2, 3, 4, 5, 7], k = 2 \
Output: [-9, -7, 7, -4, 0, 5, 3, 4, 2, 2]

[move element to the end](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/MoveElementToTheEnd.kt)

```kotlin
// O(n) time | O(1) space
fun moveElementToTheEnd(arr: MutableList<Int>, k: Int) {
    var low = 0
    var high = arr.size - 1

    while (low < high) {
        if (arr[low] == k) {
            while (low < high && arr[high] == k) high--
            swap(arr, low, high--)
        }
        low++
    }
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}
```
