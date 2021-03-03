---
title: "Palindrome Check"
date: 2021-03-03T16:56:50+03:00
draft: true
---

Палиндром - строка, которая одинаково читается в обоих направлениях.

[palindrome check](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/PalindromeCheck.kt)

```kotlin
// O(n) time | O(1) space
fun isPalindrome(s: String): Boolean {
    for (i in s.indices) {
        if (s[i] != s[s.length - 1 - i]) {
            return false
        }
    }
    return true
}
```
