---
title: "Remove Duplicates From Linked List"
date: 2021-06-02T20:04:39+03:00
draft: true
categories: ["linked list"]
---

Input: [1, 1, 1, 2, 2, 3] \
Output: [1, 2, 3]

[remove duplicates from linked list](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/linked_list/RemoveDuplicatedFromLinkedList.kt)

```kotlin
class ListNode(var value: Int) {
    var next: ListNode? = null
}

// O(n) time | O(1) space
fun removeDuplicatesFromLinkedList(linkedList: ListNode): ListNode {
    var curr: ListNode? = linkedList
    while (curr != null) {
        var next = curr.next
        while (next != null && next.value == curr.value) {
            next = next.next
        }
        curr.next = next
        curr = next
    }

    return linkedList
}
```
