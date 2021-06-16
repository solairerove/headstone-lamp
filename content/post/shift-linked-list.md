---
title: "Shift Linked List"
date: 2021-06-16T14:45:29+03:00
draft: true
categories: ["linked list"]
---

Input: [1, 2, 3, 4, 5], 2 \
Output: [4, 5, 1, 2, 3]

[shift linked list](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/linked_list/ShiftLinkedList.kt)

```kotlin
open class ListNode(var value: Int) {
    var next: ListNode? = null
}

// O(n) time | O(1) space
fun shiftLinkedList(head: ListNode, k: Int): ListNode {
    var length = 1
    var tail = head
    while (tail.next != null) {
        tail = tail.next!!
        length++
    }

    val shift = abs(k) % length
    if (shift == 0) return head
    val newPosition = if (k > 0) length - shift else shift
    var newTail = head
    for (i in 1 until newPosition) {
        newTail = newTail.next!!
    }

    val newHead = newTail.next!!
    newTail.next = null
    tail.next = head

    return newHead
}
```
