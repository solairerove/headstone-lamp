---
title: "Generate Document"
date: 2021-05-19T09:09:38+03:00
draft: true
categories: ["strings"]
---

Input: chars = "abcabc", doc = "aabbcc" \
Output: true

[generate document](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/GenerateDocument.kt)

```kotlin
// O(n + m) time | O(c) space
// n is number of chars
// m is document length
// c is number of unique chars
fun generateDocument(chars: String, doc: String): Boolean {
    val freq = mutableMapOf<Char, Int>()

    for (c in chars) {
        if (c !in freq) freq[c] = 0
        freq[c] = freq[c]!! + 1
    }

    for (c in doc) {
        if (c !in freq || freq[c] == 0) return false
        freq[c] = freq[c]!! - 1
    }

    return true
}
```
