---
title: "Sort K Sorted Array"
date: 2021-04-22T23:48:43+03:00
draft: true
categories: ["heap"]
---

Input: arr = [6, 5, 3, 2, 8, 10, 9], k = 3 \
Output: [2, 3, 5, 6, 8, 9, 10]

[merge k sorted arrays](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/heap/MergeKSortedArrays.kt)
[min heap](https://solairerove.github.io/post/min-heap/)

```kotlin
// O(nlog(k)) time | O(k) space
// n - total elements, k is k
fun sortKSortedArrays(arr: MutableList<Int>, k: Int) {
    val minHeap = MinHeap(arr.slice(0..min(k, arr.size - 1)).toMutableList())

    var idx = 0
    for (i in k + 1 until arr.size) {
        arr[idx++] = minHeap.remove()
        minHeap.insert(arr[i])
    }

    while (minHeap.size() != 0) {
        arr[idx++] = minHeap.remove()
    }
}
```
