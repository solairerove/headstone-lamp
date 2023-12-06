---
title: 242. Valid Anagram
description: count the occurrences of each character in both strings and then compare the counts.
date: 2023-10-24
tags: [ arrays, easy ] 
---

```python
# O(n) time || O(1) space
def is_anagram(self, s: str, t: str) -> bool:
    if len(s) != len(t):
        return False

    cnt = [0] * 26
    for i in range(len(s)):
        cnt[ord(s[i]) - ord('a')] += 1
        cnt[ord(t[i]) - ord('a')] -= 1

    return max(cnt) == 0
```

```python
# O(n) time || O(n) space
def is_anagram_counter(self, s: str, t: str) -> bool:
    return collections.Counter(s) == collections.Counter(t)
```

Efficient method is to count the occurrences of each character in both strings and then compare the counts.
