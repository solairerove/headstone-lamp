---
title: "Binary Search"
date: 2021-02-25T17:32:26+03:00
draft: true
---

Бинарный поиск - алгоритм, на вход которого подается отсортированный список элементов.
Если искомый элемент присутствует, то бинарный поиск возвращает его позицию. 

Предположим, что вы загадали число от 1 до 100. 
При каждой попытке угадать я буду давать один из трех ответов: много, мало и угадал.
Можно перебирать все вариант подряд: 1, 2, 3, 4.
А можно исключить сразу половину чисел на каждом шаге: 50, 75, 63.

[binary search](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/BinarySearch.kt)

```kotlin
// O(log(n)) time | O(1) space
private fun binarySearch(items: List<Int>, item: Int): Int {
    // храним границы части списка, в которой выполняется поиск
    var low = 0
    var high = items.size - 1

    // пока часть списка не сократится до элемента
    while (low <= high) {
        val mid = (low + high) / 2 // берем средний элемент
        val guess = items[mid]

        when {
            guess == item -> return mid // значение найдено
            guess > item -> high = mid - 1 // много
            else -> low = mid + 1 // мало
        }
    }

    return -1 // не найдено
}
```
