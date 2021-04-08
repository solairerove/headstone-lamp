---
title: "Count Sort"
date: 2021-04-09T00:11:24+03:00
draft: true
categories: ["sorting"]
---

Сортировка подсчетом. \
Считаем количество вхождений каждого элемента. \
Потом куммулятивную сумму и так находим нужную позицию элемента.

[count sort](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/CountSort.kt)

```kotlin
// O(n + m) time | O(n) space
fun countSort(arr: MutableList<Int>) {
    val n = arr.size

    // find max
    var max = arr[0]
    arr.forEach { if (it > max) max = it }

    // init count with zeros
    val count = MutableList(max + 1) { 0 }

    // count
    arr.forEach { count[it]++ }

    // cumulate sum
    for (i in 1..max) {
        count[i] += count[i - 1]
    }

    val output = MutableList(n + 1) { 0 }
    for (i in n - 1 downTo 0) {
        output[count[arr[i]] - 1] = arr[i]
        count[arr[i]]--
    }

    arr.forEachIndexed { i, _ -> arr[i] = output[i] }
}
```
