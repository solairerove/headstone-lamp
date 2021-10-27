---
title: "Inorder Successor"
date: 2021-10-27T13:49:10+03:00
draft: true
categories: ["binary tree"]
---

In Binary Tree, Inorder successor of a node is the next node in Inorder traversal of the Binary Tree

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Input: 7
Output: 15

[inorder successor](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/InorderSuccessor.kt) \
[leetcode](https://leetcode.com/problems/inorder-successor-in-bst/)

No clue

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
    val parent: TreeNode? = null
}

// O(h) time | O(1) space
fun inorderSuccessor(node: TreeNode): TreeNode? {
    if (node.right != null) return getLeftmostLeaf(node.right!!)

    return getRightmostParent(node)
}

fun getLeftmostLeaf(node: TreeNode): TreeNode {
    var curr = node
    while (curr.left != null) {
        curr = curr.left!!
    }

    return curr
}

fun getRightmostParent(node: TreeNode): TreeNode? {
    var curr = node
    while (curr.parent != null && curr.parent!!.right == curr) {
        curr = curr.parent!!
    }

    return curr.parent
}
```
