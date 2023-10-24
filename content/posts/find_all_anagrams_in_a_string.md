---
title: 438. Find All Anagrams in a String
description: sliding window - decrement the count of the character that is left behind i - len(p)
date: 2023-10-24
tags: [ array, medium ] 
---

```python
# O(n) time | O(1) space
def find_anagrams(self, s: str, p: str) -> List[int]:
    s_cnt, p_cnt = [0] * 26, [0] * 26

    for c in s[:len(p)]:
        s_cnt[ord(c) - ord('a')] += 1

    for c in p:
        p_cnt[ord(c) - ord('a')] += 1

    res = []
    if s_cnt == p_cnt:
        res.append(0)

    for i in range(len(p), len(s)):
        s_cnt[ord(s[i]) - ord('a')] += 1
        s_cnt[ord(s[i - len(p)]) - ord('a')] -= 1
        if s_cnt == p_cnt:
            res.append(i - len(p) + 1)

    return res
```

1) Initialization:
    - First, set up two lists of size 26 (assuming lowercase English letters) to act as frequency tables for `p` and the current window in `s`.
    - Initialize a list result to store the starting indices of the anagrams in `s`.
2) Setup:
   - Count the frequency of each character in `p` and store it in the frequency table for `p`.
   - Count the frequency of characters in the initial window of `s` (i.e., the first `len(p)` characters) and store it in the frequency table for `s`.
3) Sliding Window:
   - Iterate from `i = len(p)` to `len(s)`. For each `i`:
     - Compare the two frequency tables. If they are the same, the current window is an anagram of `p`, so append `i - len(p)` to result.
     - Slide the window: decrement the count of the character that is left behind `i - len(p)` and increment the count of the new `i` character.
