---
title: "Radix Sort"
date: 2021-04-21T22:09:42+03:00
draft: true
categories: ["sorting"]
---

[radix sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/RadixSort.kt)

```kotlin
// O(d * (n + m)) time | O(n + m) space
fun radixSort(arr: MutableList<Int>) {
    // find max
    var max = arr[0]
    arr.forEach { if (it > max) max = it }

    var digit = 0
    while (max / 10.0.pow(digit).toInt() > 0) {
        countSort(arr, digit++)
    }
}

fun countSort(arr: MutableList<Int>, digit: Int) {
    // init count with zeros
    val count = MutableList(10) { 0 }

    // count
    val digitColumn = 10.0.pow(digit).toInt()
    for (el in arr) {
        val countIdx = (el / digitColumn) % 10
        count[countIdx]++
    }

    // cumulate sum
    for (i in 1..9) {
        count[i] += count[i - 1]
    }

    val n = arr.size
    val output = MutableList(n) { 0 }
    for (i in n - 1 downTo 0) {
        val cntIdx = (arr[i] / digitColumn) % 10
        val outputIdx = --count[cntIdx]
        output[outputIdx] = arr[i]
    }

    arr.forEachIndexed { i, _ -> arr[i] = output[i] }
}
```
