---
title: "Inversions"
date: 2021-03-31T23:10:38+03:00
draft: true
categories: ["sorting"]
---

Вытекающая задача из сортировки слиянием. \

[3.2 Подсчет инверсий](https://storage.piter.com/upload/contents/978544610907/978544610907_p.pdf)

[inversions](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/Inversions.kt)

```kotlin
// O(nlog(n)) time | O(n) space
fun count(arr: MutableList<Int>): Long {
    val n = arr.size
    val b = MutableList(n) { i -> i }
    val aux = MutableList(n) { i -> i }

    for (i in 0 until n) {
        b[i] = arr[i]
    }

    return count(arr, b, aux, 0, n - 1)
}

fun count(arr: MutableList<Int>, b: MutableList<Int>, aux: MutableList<Int>, low: Int, high: Int): Long {
    var inversions = 0L

    if (high <= low) {
        return 0
    }

    val mid = low + (high - low) / 2

    inversions += count(arr, b, aux, low, mid)
    inversions += count(arr, b, aux, mid + 1, high)
    inversions += merge(b, aux, low, mid, high)

    return inversions
}

fun merge(arr: MutableList<Int>, aux: MutableList<Int>, low: Int, mid: Int, high: Int): Long {
    var inversions = 0L

    for (k in low..high) {
        aux[k] = arr[k]
    }

    var i = low
    var j = mid + 1

    for (k in low..high) {
        when {
            i > mid -> arr[k] = aux[j++]
            j > high -> arr[k] = aux[i++]
            aux[j] < aux[i] -> {
                arr[k] = aux[j++]
                inversions += (mid - i + 1)
            }
            else -> arr[k] = aux[i++]
        }
    }

    return inversions
}
```
