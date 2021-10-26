---
title: "Find Kth Largest Element in a BST"
date: 2021-10-26T11:19:53+03:00
draft: true
categories: ["binary search tree"]
---

        14
       /  \
      7   21
     /\   /\
    3  8 15 25

Input: 2
Output: 21

Input: 4
Output: 14

[find kth largest element in a bst](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/FindKthLargestElementInABST.kt) \
[leetcode](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

Make in order tree traversal, so kth largest will be `arr.size - k`

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

// O(n) time | O(n) space
fun findKLargestValue(node: BSTNode, k: Int): Int {
    val arr = mutableListOf<Int>()
    inOrderTraversal(node, arr)
    return arr[arr.size - k]
}

// O(n) time | O(n) space
fun inOrderTraversal(node: BSTNode?, arr: MutableList<Int>) {
    if (node != null) {
        inOrderTraversal(node.left, arr)
        arr.add(node.value)
        inOrderTraversal(node.right, arr)
    }
}
```
