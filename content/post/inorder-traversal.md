---
title: "Binary Tree Inorder Traversal"
date: 2021-11-11T11:48:23+03:00
draft: true
categories: ["binary tree"]
---

Given the root of a binary tree, return the inorder traversal of its nodes' values.

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: [14, 7, 15, 3, 21, 8, 25]

[inorder traversal](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/InorderTraversal.kt) \
[leetcode](https://leetcode.com/problems/binary-tree-inorder-traversal/)

No clue

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
    val parent: TreeNode? = null
}

// O(n) time | O(n) space
fun inorderTraversal(root: TreeNode?, arr: MutableList<Int> = mutableListOf()): List<Int> {
    if (root != null) {
        inorderTraversal(root.left, arr)
        arr.add(root.value)
        inorderTraversal(root.right, arr)
    }
    return arr
}
```
