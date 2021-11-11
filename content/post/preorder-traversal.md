---
title: "Binary Tree Preorder Traversal"
date: 2021-11-11T11:50:53+03:00
draft: true
categories: ["binary tree"]
---

Given the root of a binary tree, return the preorder traversal of its nodes' values.

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: [3, 7, 14, 15, 8, 21, 25]

[preorder traversal](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/PreorderTraversal.kt) \
[leetcode](https://leetcode.com/problems/binary-tree-preorder-traversal/)

No clue

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
    val parent: TreeNode? = null
}

// O(n) time | O(n) space
fun preorderTraversal(root: TreeNode?, arr: MutableList<Int> = mutableListOf()): List<Int> {
    if (root != null) {
        arr.add(root.value)
        preorderTraversal(root.left, arr)
        preorderTraversal(root.right, arr)
    }
    return arr
}
```
