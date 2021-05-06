---
title: "Non Constructable Change"
date: 2021-05-06T13:40:20+03:00
draft: true
categories: ["arrays"]
---

Input: arr = [2, 3, 1, 1, 2, 13] \
Output: 10

[non constructable change](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/NonConstructableChange.kt)

```kotlin
// O(nlog(n)) time | O(1) space
fun nonConstructableChange(arr: MutableList<Int>): Int {
    arr.sort()

    var change = 0
    for (el in arr) {
        if (el > change + 1) return change + 1

        change += el
    }

    return change + 1
}
```
