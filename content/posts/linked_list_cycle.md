---
title: 141. Linked List Cycle
description: easy
date: 2023-10-18
tags: [ linked-list, grind-169 ] 
---

```python
# O(n) time || O(1) space
def has_cycle(self, head: Optional[ListNode]) -> bool:
    slow = fast = head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
        if slow == fast:
            return True

    return False
```

`Floyd's Cycle Finding` Algorithm by considering two pointers at different speed. \
The `slow` pointer moves one step at a time while the `fast` pointer moves two steps at a time.
