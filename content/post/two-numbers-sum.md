---
title: "Two Numbers Sum"
date: 2021-04-12T22:06:31+03:00
draft: true
categories: ["arrays"]
---

Дан массив. Вернуть массив из элементов, сумма которых равна заданной. \

- Наивный подход на n^2 пересуммировать все возможные элементы. \
- Линейная сложность с помощью мапы или сета. \
- Константную память можно получить, \
если отсортировать массив, \
и почти как в бинарном поиске обновлять верхний и нижний индексы 

[two number sum](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/TwoNumberSum.kt)

```kotlin
// O(n) time | O(n) space
fun twoNumberSumSet(arr: MutableList<Int>, targetSum: Int): List<Int> {
    val numbers = hashSetOf<Int>()

    for (a in arr) {
        val potential = targetSum - a
        if (numbers.contains(potential)) {
            return listOf(a, potential)
        } else {
            numbers.add(a)
        }
    }

    return listOf()
}

// O(nlog(n)) time | O(1) space
fun twoNumberSumSort(arr: MutableList<Int>, targetSum: Int): List<Int> {
    var low = 0
    var high = arr.size - 1

    while (low < high) {
        val potentialSum = arr[low] + arr[high]

        when {
            potentialSum < targetSum -> low++
            potentialSum > targetSum -> high--
            else -> return listOf(arr[low], arr[high])
        }
    }

    return listOf()
}
```
