---
title: 13. Roman to Integer
description: if current bigger or equal then previous -> make sum, otherwise subtract
date: 2023-12-04
tags: [ arrays, math, easy ] 
---

```python
# O(1) time || O(1) space
def roman_to_int(self, s: str) -> int:
    roman = {"I": 1, "V": 5, "X": 10, "L": 50, "C": 100, "D": 500, "M": 1000, "Z": 0}
    res = 0
    s = s + "Z"
    for i in range(1, len(s)):
        if roman[s[i]] <= roman[s[i - 1]]:
            res += roman[s[i - 1]]
        else:
            res -= roman[s[i - 1]]

    return res
```

here's trick. start from `1` element. if previous is bigger or equal add prev, in other case subtract it.
result will be sum/subtract. to make such calculation easier, add `Z=0` in the end of the string. 
