---
title: "Bubble Sort"
date: 2021-03-01T14:33:33+03:00
draft: true
categories: ["sorting"]
---

Один из не эффективных алгоритмов сортировки, кроме случая, когда коллекция обратно отсортирована.
На каждом шаге проталкивает самый большой элемент в конец списка.

[bubble sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/BubbleSort.kt)

```kotlin
// O(n^2) time | O(1) space
fun bubbleSort(arr: MutableList<Int>) {
    val n = arr.size

    for (i in 0 until n) {
        for (j in 0 until (n - i - 1)) {
            if (arr[j + 1] < arr[j]) {
                swap(arr, j + 1, j)
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
