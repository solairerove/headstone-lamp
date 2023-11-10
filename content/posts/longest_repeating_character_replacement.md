---
title: 424. Longest Repeating Character Replacement
description: check if length of `substring - max_freq` does not exceed k
date: 2023-11-10
tags: [ sliding-window, medium ] 
---

```python
# O(n) time | O(1) space
def character_replacement(self, s: str, k: int) -> int:
    freq, max_freq, res = collections.defaultdict(int), 0, 0
    low = 0
    for high in range(len(s)):
        freq[s[high]] += 1
        max_freq = max(max_freq, freq[s[high]])

        if (high - low + 1) - max_freq > k:
            freq[s[low]] -= 1
            low += 1

        res = max(res, high - low + 1)

    return res
```

### Detailed Explanation:

1) #### Initialize Variables:

    - `freq`: A dictionary to store the frequency of each character in the current window.
    - `max_freq`: Tracks the maximum frequency of any character in the current window.
    - `low`: Pointer for the start of the window.
    - `res`: Keeps track of the maximum length of a valid window seen so far.

2) #### Iterate Through the String:

    - We use a for loop to iterate through the string, with `high` as the end pointer of the window.
    - At each step, we include the character at the `high` position in our window and update its `freq` in the count
      dictionary.
    - We update `max_freq` to reflect the highest frequency of any character in the current window.

3) #### Validate the Window:

    - A window is valid if the number of replacements required to make all characters in it the same does not
      exceed `k`.
      This is checked by the condition `(high - low + 1) - max_freq > k`, which calculates the number of characters that
      are different from the most frequent character.
    - If the window becomes invalid, we shrink it from the `low` by increasing the left pointer and updating the count
      of the character at the `low` position.

4) #### Update Maximum Length:

    - If the window is valid, we update `res` to be the maximum of its current value and the size of the current
      window.