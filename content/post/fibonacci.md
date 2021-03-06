---
title: "Fibonacci"
date: 2021-03-02T11:33:16+03:00
draft: true
categories: ["recursion"]
---

Один из классических рекурсивных алгоритмов.
Последовательность чисел, где каждое последующее - сумма двух предыдущих.

[fibonacci](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/recursion/Fibonacci.kt)

```kotlin
// O(n) time | O(1) space
fun getNthFibonacci(n: Int): Int {
    val lastTwo = mutableListOf(0, 1)

    repeat(n - 2) {
        val next = lastTwo.sum()
        lastTwo[0] = lastTwo[1]
        lastTwo[1] = next
    }

    return if (n > 1) lastTwo[1] else lastTwo[0]
}
```
