---
title: "Product Sum"
date: 2021-05-21T14:12:31+03:00
draft: true
categories: ["recursion"]
---

Input: [1, [2, [3]]] \
Output: 23

[product sum](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/recursion/ProductSum.kt)

```kotlin
// O(n) time | O(d) space
// n is total number of elements
// d is max depth
fun productSum(arr: List<*>): Int {
    return productSum(arr, 1)
}

fun productSum(arr: List<*>, multiplier: Int): Int {
    var sum = 0

    for (el in arr) {
        sum += if (el is List<*>) {
            productSum(el, multiplier + 1)
        } else {
            el as Int
        }
    }

    return sum * multiplier
}
```
