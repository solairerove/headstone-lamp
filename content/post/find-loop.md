---
title: "Find Loop"
date: 2021-06-09T17:31:41+03:00
draft: true
categories: ["linked list"]
---

Input:
```
1 -> 2 -> 3
|    |
5 <- 4
```
Output: 2

[find loop](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/linked_list/FindLoop.kt)

```kotlin
class ListNode(var value: Int) {
    var next: ListNode? = null
}

// O(n) time | O(1) space
fun findLoop(head: ListNode?): ListNode? {
    var first = head?.next
    var second = first?.next
    while (first != second) {
        first = first?.next
        second = second?.next?.next
    }
    first = head
    while (first != second) {
        first = first?.next
        second = second?.next
    }

    return first
}
```
