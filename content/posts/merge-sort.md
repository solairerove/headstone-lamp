---
title: "Merge Sort"
date: 2021-03-26T17:28:02+03:00
draft: true
---

Классический эффективный алгоритм сортировки divide and conquer. \
Разделяем массив на подмассивы до подмассивов размером 1 и \
собираем их в отсортированные подмассивы.

Почему O(nlog(n)). \
Потому что у нас всего nlog(n) операций, которые сами по себе O(n).


[merge sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/MergeSort.kt)

```kotlin
// O(nlog(n)) time | O(n) space
fun mergeSort(arr: MutableList<Int>) {
    val n = arr.size

    val aux = MutableList(n) { i -> i }
    mergeSort(arr, aux, 0, n - 1)
}

fun mergeSort(arr: MutableList<Int>, aux: MutableList<Int>, low: Int, high: Int) {
    if (high <= low) {
        return
    }

    val mid = low + (high - low) / 2

    mergeSort(arr, aux, low, mid)
    mergeSort(arr, aux, mid + 1, high)
    merge(arr, aux, low, mid, high)
}

fun merge(arr: MutableList<Int>, aux: MutableList<Int>, low: Int, mid: Int, high: Int) {
    var i = low
    var j = mid + 1

    for (k in low..high) {
        aux[k] = arr[k]
    }

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
