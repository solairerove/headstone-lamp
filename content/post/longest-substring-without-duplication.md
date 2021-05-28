---
title: "Longest Substring Without Duplication"
date: 2021-05-28T17:56:39+03:00
draft: true
categories: ["strings"]
---

Input: "qvfwpccitm" \
Output: "qvfwpc" \

[longest substring without duplication](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/LongestSubstringWithoutDuplication.kt)

```kotlin
// O(n) time | O(n) space
fun longestSubstringWithoutDuplication(s: String): String {
    val charToLastIdx = mutableMapOf<Char, Int>()
    var longest = Pair(0, 1)
    var low = 0
    for (i in s.indices) {
        val char = s[i]
        if (char in charToLastIdx) {
            low = max(low, charToLastIdx[char]!! + 1)
        }

        if (i + 1 - low > longest.second - longest.first) {
            longest = Pair(low, i + 1)
        }

        charToLastIdx[char] = i
    }

    return s.substring(longest.first, longest.second)
}
```
