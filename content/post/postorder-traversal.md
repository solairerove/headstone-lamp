---
title: "Binary Tree Postorder Traversal"
date: 2021-11-11T11:55:00+03:00
draft: true
categories: ["binary tree"]
---

Given the root of a binary tree, return the postorder traversal of its nodes' values.

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: [14, 15, 7, 21, 25, 8, 3]

[postorder traversal](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/PostorderTraversal.kt) \
[leetcode](https://leetcode.com/problems/binary-tree-postorder-traversal/)

No clue

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
    val parent: TreeNode? = null
}

// O(n) time | O(n) space
fun postorderTraversal(root: TreeNode?, arr: MutableList<Int> = mutableListOf()): List<Int> {
    if (root != null) {
        postorderTraversal(root.left, arr)
        postorderTraversal(root.right, arr)
        arr.add(root.value)
    }
    return arr
}
```
