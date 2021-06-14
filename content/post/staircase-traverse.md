---
title: "Staircase Traverse"
date: 2021-06-14T21:34:18+03:00
draft: true
categories: ["recursion"]
---

Input: 4 3 \
Output: 7

[staircase traverse](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/recursion/StaircaseTraverse.kt)

```kotlin
// O(n) time | O(n) space
fun staircaseTraverse(height: Int, maxSteps: Int): Int {
    var number = 0
    val ways = mutableListOf(1)

    for (curr in 1 until height + 1) {
        val low = curr - maxSteps - 1
        val high = curr - 1
        if (low >= 0) number -= ways[low]

        number += ways[high]
        ways.add(number)
    }

    return ways[height]
}
```
