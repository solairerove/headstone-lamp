---
title: 844. Backspace String Compare
description: compare reversed string with `#` times skip
date: 2023-10-19
tags: [ two-pointers, arrays, easy ]
---

```python
# O(n + m) time || O(1) space
def backspace_compare_two_pointers(self, s: str, t: str) -> bool:
    def trim(to_trim):
        skip = 0
        for c in reversed(to_trim):
            if c == '#':
                skip += 1
            elif skip:
                skip -= 1
            else:
                yield c

    return all(a == b for a, b in itertools.zip_longest(trim(s), trim(t)))
```

```python
# O(n + m) time || O(n + m) space
def backspace_compare_stack(self, s: str, t: str) -> bool:
    def trim(line):
        stack = []
        for c in line:
            if c != '#':
                stack.append(c)
            elif stack:
                stack.pop()

        return "".join(stack)

    return trim(s) == trim(t)
```

one approach is using stack. \
the main approach is literally the name of the problem. \
write a method that traverse reversed string and skip chars # times. \
compare each symbol from two strings using above method.
