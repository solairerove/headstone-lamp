---
title: "Sum of Linked Lists"
date: 2021-06-11T16:53:53+03:00
draft: true
categories: ["linked list"]
---

Input: [1 2 3 4 5 6] [7 8 9 10]
Output: [8 0 3 5 6 6]

[sum of linked lists](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/linked_list/SumOfLinkedLists.kt)

```kotlin
class ListNode(var value: Int) {
    var next: ListNode? = null
}

// O(max(n + m)) time | O(max(n + m)) space
fun sumOfLinkedLists(headFirst: ListNode, headSecond: ListNode): ListNode {
    val newHead = ListNode(0)
    var curr = newHead
    var carry = 0

    var nodeOne: ListNode? = headFirst
    var nodeTwo: ListNode? = headSecond
    while (nodeOne != null || nodeTwo != null || carry != 0) {
        val valueOne = nodeOne?.value ?: 0
        val valueTwo = nodeTwo?.value ?: 0
        val sum = valueOne + valueTwo + carry

        val newValue = sum % 10
        val newNode = ListNode(newValue)
        curr.next = newNode
        curr = newNode

        carry = sum / 10
        nodeOne = nodeOne?.next
        nodeTwo = nodeTwo?.next
    }
    return newHead.next!!
}
```
