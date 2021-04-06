---
title: "Quick Sort 3 Way"
date: 2021-04-06T20:10:04+03:00
draft: true
categories: ["sorting"]
---

Вариант быстрой сортировки с трехчастным разбиением для массивов с низкой энтропией.

`a[low]..a[lt - 1] <= a[j] <= a[gt + 1]..a[high]`
`a[lt - 1] = a[j] = a[gt + 1]`

[princeton quicksort 3 way](https://algs4.cs.princeton.edu/code/edu/princeton/cs/algs4/Quick3way.java.html)

[quick sort 3 way](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/QuickSort3Way.kt)

```kotlin
// O(nlog(n)) time | O(log(n)) space
fun quickSort(arr: MutableList<Int>, low: Int = 0, high: Int = arr.size - 1) {
    if (high <= low) return
    var lt = low
    var gt = high
    val v = arr[low]
    var i = low + 1

    while (i <= gt) {
        when {
            arr[i] < v -> swap(arr, lt++, i++)
            arr[i] > v -> swap(arr, i, gt--)
            else -> i++
        }
    }

    quickSort(arr, low, lt - 1)
    quickSort(arr, gt + 1, high)
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}
```
