---
title: 20. Valid Parentheses
description: traverse string, use stack and close to open bracket mapping
date: 2023-10-26
tags: [ arrays, stack, easy ]
---

```python
# O(n) time || O(n) space
def is_valid(self, s: str) -> bool:
    brackets = {')': '(', ']': '[', '}': '{'}
    stack = []
    for br in s:
        if br in brackets:
            if not stack or stack.pop() != brackets[br]:
                return False
        else:
            stack.append(br)

    return not stack
```

1) Initialize an empty stack.
2) Traverse the string character by character.
3) For each character:
    - If it's an open bracket ('(', '{', or '['), push it onto the stack.
    - If it's a closing bracket, check the top of the stack:
        - If the stack is empty, the string is not valid.
        - If the top of the stack is not the corresponding open bracket, the string is not valid.
        - If the top of the stack is the corresponding open bracket, pop the stack.
4) After traversing the string, if the stack is not empty, the string is not valid.
5) If we pass the above checks, the string is valid.
