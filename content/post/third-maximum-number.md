---
title: "Third Maximum Number"
date: 2021-04-15T22:56:13+03:00
draft: true
categories: ["search"]
---

[leetcode](https://leetcode.com/problems/third-maximum-number/)

[third maximum number](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/searching/ThirdMaximumNumber.kt)

```kotlin
// O(n) time | O(1) space
fun thirdMaximumNumber(arr: List<Int>): Int {
    val largestNumbers = mutableListOf(Int.MIN_VALUE, Int.MIN_VALUE, Int.MIN_VALUE)

    for (element in arr) {
        when {
            element > largestNumbers[2] -> shift(largestNumbers, element, 2)
            element > largestNumbers[1] -> shift(largestNumbers, element, 1)
            element > largestNumbers[0] -> shift(largestNumbers, element, 0)
        }
    }

    return largestNumbers[0]
}

fun shift(arr: MutableList<Int>, toInsert: Int, position: Int) {
    for (i in 0 until position + 1) {
        arr[i] = if (i == position) toInsert else arr[i + 1]
    }
}
```
