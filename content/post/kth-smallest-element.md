---
title: "Kth Smallest Element in a BST"
date: 2021-11-11T14:17:20+03:00
draft: true
categories: ["binary search tree"]
---

Given the root of a binary search tree, and an integer k, \
return the kth smallest value (1-indexed) of all the values of the nodes in the tree.

        14
       /  \
      7   21
     /\   /\
    3  8 15 25

Input: 2
Output: 7

[kth smallest element](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/KthSmallestElement.kt) \
[leetcode](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

Make inorder tree traversal, so kth largest will be `arr[k - 1]`

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

// O(n) time | O(n) space
fun kthSmallest(root: BSTNode?, k: Int): Int {
    val arr = mutableListOf<Int>()
    inorderTraversal(root, arr)
    return arr[k - 1]
}

fun inorderTraversal(root: BSTNode?, arr: MutableList<Int>) {
    if (root != null) {
        inorderTraversal(root.left, arr)
        arr.add(root.value)
        inorderTraversal(root.right, arr)
    }
}
```
