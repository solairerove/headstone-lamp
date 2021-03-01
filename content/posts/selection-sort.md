---
title: "Selection Sort"
date: 2021-03-01T13:40:33+03:00
draft: true
---

Один из не эффективных алгоритмов сортировки.
На каждом шаге находит минимальный элемент и меняет местами с текущим.

[selection sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/SelectionSort.kt)

```kotlin
// O(n^2) time | O(1) space
fun selectionSort(arr: MutableList<Int>) {
    val n = arr.size

    for (i in 0 until n) {
        var min = i

        for (j in (i + 1) until n) {
            if (arr[j] < arr[min]) {
                min = j
            }
        }

        swap(arr, i, min)
    }
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}
```
