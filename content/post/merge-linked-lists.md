---
title: "Merge Linked Lists"
date: 2021-06-10T18:08:37+03:00
draft: true
categories: ["linked list"]
---

Input: [1 2 3 4 5 6] [7 8 9 10]
Output: [1 2 3 4 5 6 7 8 9 10]

[merge linked lists](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/linked_list/MergeLinkedLists.kt)

```kotlin
class ListNode(var value: Int) {
    var next: ListNode? = null
}

// O(n + m) time | O(1) space
fun mergeLinkedLists(headFirst: ListNode, headSecond: ListNode): ListNode {
    var i: ListNode? = headFirst
    var prev: ListNode? = null
    var j: ListNode? = headSecond
    while (i != null && j != null) {
        if (i.value < j.value) {
            prev = i
            i = i.next
        } else {
            if (prev != null) prev.next = j
            prev = j
            j = j.next
            prev.next = i
        }
    }

    if (i == null) prev?.next = j
    return if (headFirst.value < headSecond.value) headFirst else headSecond
}
```
