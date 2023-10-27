---
title: 5. Longest Palindromic Substring
description: a common approach is to expand around the center
date: 2023-10-27
tags: [ arrays, two-pointers, medium ]
---

```python
# O(n^2) time || O(1) space
def longest_palindrome(self, s: str) -> str:
    def get_palindrome_from(low, high):
        while low >= 0 and high < len(s) and s[low] == s[high]:
            low, high = low - 1, high + 1

        return s[low + 1: high]

    return max([get_palindrome_from(i, j) for i in range(len(s)) for j in (i, i + 1)], key=len)
```

This problem can be solved using several methods. A common approach is to expand around the center. This approach can
handle even and odd length palindromes well. Here's the idea:

For every character in the string:

1) Consider the character as the center of an odd-length palindrome and expand outwards.
2) Consider the character and its next character as the center of an even-length palindrome and expand outwards.
3) Record the longest palindrome found.
