---
title: 2. Add Two Numbers
description: medium
date: 2023-10-18
tags: [ linked-list, grind-169 ] 
---

```python
# O(max(n, m)) time || O(1) space
def add_two_numbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
    sentinel = ListNode()
    prev = sentinel

    hold = 0
    while l1 or l2:
        curr_sum = 0

        if l1:
            curr_sum, l1 = curr_sum + l1.val, l1.next

        if l2:
            curr_sum, l2 = curr_sum + l2.val, l2.next

        curr_sum += hold

        prev.next, hold = ListNode(curr_sum % 10), curr_sum // 10
        prev = prev.next

    if hold:
        prev.next = ListNode(hold)

    return sentinel.next
```

calculate sum in column like in school. use on hold var. \
`sum % 10` is value, `sum // 10` is in memory. \
it's better to traverse `while l1 or l2:` to avoid building list from left part of list.
