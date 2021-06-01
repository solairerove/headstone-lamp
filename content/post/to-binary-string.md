---
title: "To Binary String"
date: 2021-06-01T21:25:18+03:00
draft: true
categories: ["strings"]
---

Input: "10" \
Output: "1010"

[to binary string](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/ToBinaryString.kt)

```kotlin
// O(n) time | O(n) space
fun toBinaryString(n: Int): String {
    val stringBuilder = StringBuilder()
    var idx = n
    while (idx > 0) {
        stringBuilder.insert(0, idx % 2)
        idx /= 2
    }

    return stringBuilder.toString()
}
```
