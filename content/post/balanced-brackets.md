---
title: "Balanced Brackets"
date: 2021-06-08T14:49:38+03:00
draft: true
categories: ["stack"]
---

Input: "[()]{}{[()()]()}" \
Output: true

[balanced brackets](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/stack/BalancedBrackets.kt)

```kotlin
// O(n) time | O(n) space
fun balancedBrackets(s: String): Boolean {
    val stack = Stack<Char>()

    for (i in s.indices) {
        if ('(' == s[i]) stack.push('(')
        if ('[' == s[i]) stack.push('[')
        if ('{' == s[i]) stack.push('{')

        if (')' == s[i]) {
            if (stack.isEmpty()) return false
            if ('(' != stack.pop()) return false
        }

        if (']' == s[i]) {
            if (stack.isEmpty()) return false
            if ('[' != stack.pop()) return false
        }

        if ('}' == s[i]) {
            if (stack.isEmpty()) return false
            if ('{' != stack.pop()) return false
        }
    }

    return stack.isEmpty()
}
```
