---
title: "Non Repeating Char Pivot"
date: 2021-05-20T23:08:17+03:00
draft: true
categories: ["strings"]
---

Input: "sptiroksoz" \
Output: 1

[non repeating char pivot](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/NonRepeatingCharPivot.kt)

```kotlin
// O(n) time | O(n) space
fun nonRepeatingCharPivot(s: String): Int {
    val freq = mutableMapOf<Char, Int>()

    s.forEach { freq[it] = freq.getOrDefault(it, 0) + 1 }

    for (i in s.indices) {
        if (freq[s[i]] == 1) return i
    }

    return -1
}
```
