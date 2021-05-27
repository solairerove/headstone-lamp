---
title: "Kadane"
date: 2021-05-27T19:45:49+03:00
draft: true
categories: ["arrays"]
---

Input:  [12, 11, -16, -14, -15, -9, 5, -20, 3, 7, -7] \
Output: 23

[kadane](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/Kadane.kt)

```kotlin
// O(n) time | O(1) space
fun kadane(arr: List<Int>): Int {
    var curr = arr[0]
    var max = arr[0]

    for (i in 1 until arr.size) {
        curr = max(arr[i], curr + arr[i])
        max = max(curr, max)
    }

    return max
}
```
