---
title: "Array of Products"
date: 2021-05-12T21:31:54+03:00
draft: true
categories: ["arrays"]
---

Input:  [1, 2, 3, 4, 6] \
Output: [144, 72, 48, 36, 24]

[array of products](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/ArrayOfProducts.kt)

```kotlin
// O(n) time | O(n) space
fun arrayOfProducts(arr: List<Int>): List<Int> {
    val n = arr.size
    val products = MutableList(n) { 1 }

    var low = 1
    for (i in 0 until n) {
        products[i] = low
        low *= arr[i]
    }

    var high = 1
    for (i in n - 1 downTo 0) {
        products[i] *= high
        high *= arr[i]
    }

    return products
}
```
