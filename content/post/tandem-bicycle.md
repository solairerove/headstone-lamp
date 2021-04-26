---
title: "Tandem Bicycle"
date: 2021-04-26T22:21:31+03:00
draft: true
categories: ["greedy"]
---

Найти максимальную сумму скоростей тандема велосипедистов.

Input: red = [1, 5, 9, 4, 6], blue = [4, 8, 6, 5, 3] \
Output: 34

[tandem bicycle](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/TandemBicycle.kt) \
type of [leet code](https://leetcode.com/problems/height-checker/)

```kotlin
// O(nlog(n)) time | O(1) space
fun tandemBicycle(red: MutableList<Int>, blue: MutableList<Int>): Int {
    red.sort()
    blue.sort()
    val n = red.size

    var total = 0
    for (i in 0 until n) {
        total += max(red[i], blue[n - 1 - i])
    }

    return total
}
```
