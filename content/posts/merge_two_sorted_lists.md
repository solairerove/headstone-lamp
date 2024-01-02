---
title: 21. Merge Two Sorted Lists
description: use sentinel for new list. traverse, compare and set
date: 2024-01-02
tags: [ linked-list, easy ] 
---

```python
# O(n) time || O(1) space
def merge_two_lists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
    sentinel = ListNode(-1)
    prev = sentinel
    curr1, curr2 = list1, list2
    while curr1 and curr2:
        if curr1.val <= curr2.val:
            prev.next, curr1 = curr1, curr1.next
        else:
            prev.next, curr2 = curr2, curr2.next

        prev = prev.next

    prev.next = curr1 or curr2

    return sentinel.next
```

use sentinel for result list. traverse both lists, compare which element is less. set as new node of sentinel list. do
not forget to set the end of one of lists.
