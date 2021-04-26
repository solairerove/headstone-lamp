---
title: "Merge Sort Bu"
date: 2021-04-26T21:11:12+03:00
draft: true
categories: ["sorting"]
---

[princeton mergesort](https://algs4.cs.princeton.edu/22mergesort/)

[merge sort bu](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/MergeSortBU.kt)

```kotlin
// O(nlog(n)) time | O(n) space
fun mergeSort(arr: MutableList<Int>) {
    val n = arr.size
    val aux = MutableList(n) { i -> i }

    var len = 1
    while (len < n) {
        for (low in 0 until n - len step 2 * len) {
            val mid = low + len - 1
            val high = min(low + 2 * len - 1, n - 1)
            merge(arr, aux, low, mid, high)
        }
        len *= 2
    }
}

fun merge(arr: MutableList<Int>, aux: MutableList<Int>, low: Int, mid: Int, high: Int) {
    for (k in low..high) {
        aux[k] = arr[k]
    }

    var i = low
    var j = mid + 1

    for (k in low..high) {
        when {
            i > mid -> arr[k] = aux[j++]
            j > high -> arr[k] = aux[i++]
            aux[j] < aux[i] -> arr[k] = aux[j++]
            else -> arr[k] = aux[i++]
        }
    }
}
```
