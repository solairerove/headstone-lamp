---
title: 876. Middle of the Linked List
description: traverse with slow and fast pointers, when fast reached the end, slow is the middle 
date: 2023-10-11
tags: [ linked-list, easy ] 
---

```python
# O(n) time || O(1) space
def middle_node(self, head: Optional[ListNode]) -> Optional[ListNode]:
    if not head.next:
        return head

    slow = fast = head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next

    return slow
```

`fast` pointer traverse two times faster than `slow`, \
so when `fast` is done, `slow` is in middle of lined list
