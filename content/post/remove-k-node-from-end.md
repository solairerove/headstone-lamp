---
title: "Remove K Node From End"
date: 2021-06-03T20:08:24+03:00
draft: true
categories: ["linked list"]
---

Input: [1, 1, 1, 2, 2, 3], 2 \
Output: [1, 1, 1, 2, 3]

[remove k node from end](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/linked_list/RemoveKNodeFromEnd.kt)

```kotlin
class ListNode(var value: Int) {
    var next: ListNode? = null
}

// O(n) time | O(1) space
fun removeKNodeFromEnd(head: ListNode, k: Int) {
    var cnt = 1
    var first = head
    var second: ListNode? = head

    while (cnt <= k) {
        second = second!!.next
        cnt++
    }

    if (second == null) {
        head.value = head.next!!.value
        head.next = head.next!!.next
        return
    }

    while (second!!.next != null) {
        second = second.next
        first = first.next!!
    }

    first.next = first.next!!.next
}
```
