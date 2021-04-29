---
title: "Validate Subsequence"
date: 2021-04-29T14:39:58+03:00
draft: true
categories: ["arrays"]
---

[validate subsequence](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/ValidateSubsequence.kt)

```kotlin
// O(n) time | O(1) space
fun validateSubsequence(arr: List<Int>, subsequence: List<Int>): Boolean {
    var seqIdx = 0

    for (el in arr) {
        if (seqIdx == subsequence.size) break
        if (el == subsequence[seqIdx]) seqIdx++
    }

    return seqIdx == subsequence.size
}
```
