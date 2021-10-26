---
title: "Invert Binary Tree"
date: 2021-10-26T17:15:29+03:00
draft: true
categories: ["binary tree"]
---

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

         3
       /   \
      8     7
     / \   / \
    25 21 15 14

Output: [25 8 21 3 15 7 14]

[invert binary tree](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/InvertBinaryTree.kt) \
[leetcode](https://leetcode.com/problems/invert-binary-tree)

Make recursive swap traversal.

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

fun invert(node: TreeNode?): TreeNode? {
    if (node != null) {
        swap(node)
        invert(node.left)
        invert(node.right)
    }

    return node
}

fun swap(node: TreeNode) {
    val left = node.left
    node.left = node.right
    node.right = left
}
```
