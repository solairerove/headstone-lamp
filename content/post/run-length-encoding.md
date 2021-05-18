---
title: "Run Length Encoding"
date: 2021-05-18T20:31:47+03:00
draft: true
categories: ["strings"]
---

Input: "xxxxxxyyyйййй" \
Output: "6x3y4й"

- [run length encoding](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/RunLengthEncoding.kt)

```kotlin
// O(n) time | O(n) space
fun runLengthEncoding(s: String): String {
    val n = s.length

    val encoded = mutableListOf<Char>()
    var len = 1

    for (i in 1 until n) {
        val currChar = s[i]
        val prevChar = s[i - 1]

        if (currChar != prevChar || len == 9) {
            encoded.add(len.toString()[0])
            encoded.add(prevChar)
            len = 0
        }

        len++
    }

    encoded.add(len.toString()[0])
    encoded.add(s[n - 1])

    return encoded.joinToString("")
}
```
