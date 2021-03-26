---
title: "Heap Sort"
date: 2021-03-09T17:45:39+03:00
draft: true
---

build heap from array and n time get min element. (naive heap sort)

[heap sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/HeapSort.kt)

```kotlin
// O(nlogn) time | O(1) space
fun heapSort(arr: MutableList<Int>) {
    val n = arr.size

    for (k in n / 2 downTo 1) {
        sink(arr, k, n)
    }
    var k = n
    while (k > 1) {
        swap(arr, 1, k--)
        sink(arr, 1, k)
    }
}

fun sink(arr: MutableList<Int>, k: Int, n: Int) {
    var idx = k
    while (2 * idx <= n) {
        var j = 2 * idx
        if (j < n && less(arr, j, j + 1)) j++
        if (!less(arr, idx, j)) break
        swap(arr, idx, j)
        idx = j
    }
}

fun less(arr: MutableList<Int>, i: Int, j: Int): Boolean {
    return arr[i - 1] < arr[j - 1]
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val temp = arr[i - 1]
    arr[i - 1] = arr[j - 1]
    arr[j - 1] = temp
}
```
