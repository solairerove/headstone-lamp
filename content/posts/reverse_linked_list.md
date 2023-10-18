---
title: 206. Reverse Linked List
description: easy
date: 2023-10-18
tags: [ linked-list, grind-169 ] 
---

```python
# O(n) time || O(1) space
def reverse_list(self, head: Optional[ListNode]) -> Optional[ListNode]:
    prev, curr = None, head
    while curr:
        curr.next, prev, curr = prev, curr, curr.next

    return prev
```

traverse linked list using `curr` pointer. relink `curr.next` to `prev` each step on iteration. \
return the `prev` as head of reversed list
