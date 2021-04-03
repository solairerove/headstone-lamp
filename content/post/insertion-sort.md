---
title: "Insertion Sort"
date: 2021-03-01T16:55:11+03:00
draft: true
categories: ["sorting"]
---

Один из алгоритмов сортировки.
На каждом шаге вставляет на свое место элемент в отсортированный подмассив.

[insertion sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/InsertionSort.kt)

```kotlin
// O(n^2) time | O(1) space
fun insertionSort(arr: MutableList<Int>) {
    val n = arr.size

    for (i in 1 until n) {
        for (j in i downTo 0) {
            if (j > 0 && arr[j] < arr[j - 1]) {
                swap(arr, j, j - 1)
            }
        }
    }
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}
```
