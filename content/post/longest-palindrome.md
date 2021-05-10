---
title: "Longest Palindrome"
date: 2021-05-10T20:33:20+03:00
draft: true
categories: ["strings"]
---

Input: s = "arpkqqkpfkpdp" \
Output: pkqqkp

[longest palindrome](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/LongestPalindrome.kt)

```kotlin
// O(n^2) time | O(n) space
fun longestPalindrome(s: String): String {
    var longest = listOf(0, 1)

    for (i in 1 until s.length) {
        val odd = getLongestPalindrome(s, i - 1, i + 1)
        val even = getLongestPalindrome(s, i - 1, i)
        val curr = if (odd[1] - odd[0] > even[1] - odd[0]) odd else even
        longest = if (longest[1] - longest[0] > curr[1] - curr[0]) longest else curr
    }

    return s.substring(longest[0], longest[1])
}

fun getLongestPalindrome(s: String, lowIdx: Int, highIdx: Int): List<Int> {
    var low = lowIdx
    var high = highIdx

    while (low > 0 && high < s.length) {
        if (s[low] != s[high]) break
        low--
        high++
    }

    return listOf(low + 1, high)
}
```
