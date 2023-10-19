---
title: 23. Merge k Sorted Lists
description: group by two lists and merge using problem 21
date: 2023-10-18
tags: [ linked-list, hard ] 
---

```python
# O(n * log(k)) time | O(1) space
# n - is total number of nodes
# k - is number of linked lists
def merge_k_lists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
    if not lists:
        return None

    if len(lists) == 1:
        return lists[0]

    interval = 1
    while interval < len(lists):
        for i in range(0, len(lists) - interval, interval * 2):
            lists[i] = self.merge(lists[i], lists[i + interval])
        interval *= 2

    return lists[0]


# 21. Merge Two Sorted Lists
def merge(self, l1, l2):
    sentinel = ListNode()
    prev = sentinel
    curr1, curr2 = l1, l2
    while curr1 and curr2:
        if curr1.val < curr2.val:
            prev.next, curr1 = curr1, curr1.next
        else:
            prev.next, curr2 = curr2, curr2.next

        prev = prev.next

    prev.next = curr1 or curr2

    return sentinel.next
```

at first needed to implement the problem `21. Merge Two Sorted Lists` \
then using merge method emulate merge sort using interval
