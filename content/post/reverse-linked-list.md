---
title: "Reverse Linked List"
date: 2021-04-20T19:47:52+03:00
draft: true
categories: ["linked list"]
---

[leetcode](https://leetcode.com/problems/reverse-linked-list/)

[reverse linked list](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/linked_list/ReverseLinkedList.kt)

```kotlin
class ListNode(var value: Int) {
    var next: ListNode? = null
}

// O(n) time | O(1) space
fun reverseList(head: ListNode?): ListNode? {
    var prev: ListNode? = null
    var curr: ListNode? = head

    while (curr != null) {
        val next = curr.next
        curr.next = prev
        prev = curr
        curr = next
    }

    return prev
}
```
