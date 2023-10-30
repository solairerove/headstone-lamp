---
title: 5. Longest Palindromic Substring
description: a common approach is to expand around the center
date: 2023-10-27
tags: [ arrays, two-pointers, medium ]
---

```python
# O(n^2) time || O(1) space
def longest_palindrome(self, s: str) -> str:
    def expand(i, j):
        while i >= 0 and j < len(s) and s[i] == s[j]:
            i, j = i - 1, j + 1

        return s[i + 1: j]

    return max([expand(i, j) for i in range(len(s)) for j in (i, i + 1)], key=len)
```

This problem can be solved using several methods. A common approach is to expand around the center. This approach can
handle even and odd length palindromes well. Here's the idea:

For every character in the string:

1) Consider the character as the center of an odd-length palindrome and expand outwards.
2) Consider the character and its next character as the center of an even-length palindrome and expand outwards.
3) Record the longest palindrome found.
