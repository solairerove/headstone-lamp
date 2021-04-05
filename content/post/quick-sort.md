---
title: "Quick Sort"
date: 2021-04-05T18:10:55+03:00
draft: true
categories: ["sorting"]
---

Классический эффективный алгоритм сортировки divide and conquer. \
Разбиваем массив и независимо сортируем подмассивы. \

`a[low]..a[j - 1] <= a[j] <= a[j + 1]..a[high]`

[princeton quicksort](https://algs4.cs.princeton.edu/code/edu/princeton/cs/algs4/Quick.java.html)

[quick sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/QuickSort.kt)

```kotlin
// O(nlog(n)) time | O(log(n)) space
fun quickSort(arr: MutableList<Int>) {
    quickSort(arr, 0, arr.size - 1)
}

fun quickSort(arr: MutableList<Int>, low: Int, high: Int) {
    if (high <= low) return

    val j = partition(arr, low, high)
    quickSort(arr, low, j - 1)
    quickSort(arr, j + 1, high)
}

fun partition(arr: MutableList<Int>, low: Int, high: Int): Int {
    var i = low
    var j = high + 1
    val v = arr[low]

    while (true) {
        while (arr[++i] < v) if (i == high) break
        while (v < arr[--j]) if (j == low) break
        if (i >= j) break
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
