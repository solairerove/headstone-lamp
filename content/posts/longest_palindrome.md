---
title: 409. Longest Palindrome
description: the potential length of the palindrome is len(s) - odds_cnt + bool(odds_cnt)
date: 2023-10-24
tags: [ array, easy ] 
---

```python
# O(n) time | O(1) space
def longest_palindrome(self, s: str) -> int:
    odds = sum(v % 2 for v in collections.Counter(s).values())

    return len(s) - odds + bool(odds)
```

1) Count Occurrences: Counter(s) provides the counts of each character.
2) Calculate Odds: We determine how many characters have an odd count.
3) Result: The potential length of the palindrome is len(s) - odds,
   but if there's any character with an odd count (bool(odds) will be True
   for any positive odd value), we can use one of them as the center of the palindrome.
   Hence we add 1 if odds is non-zero.
