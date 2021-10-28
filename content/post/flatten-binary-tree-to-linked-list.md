---
title: "Flatten Binary Tree to Linked List"
date: 2021-10-28T18:16:14+03:00
draft: true
categories: ["binary tree"]
---

Given the root of a binary tree, flatten the tree into a "linked list":
 - The "linked list" should use the same TreeNode class where the right child pointer points \
   to the next node in the list and the left child pointer is always null.
 - The "linked list" should be in the same order as a pre-order traversal of the binary tree.


         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: 3 -> 7 -> 14 -> 15 -> 8 -> 21 -> 25

[flatten binary tree to linked list](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/FlattenBinaryTreeToLinkedList.kt)
[leetcode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

Post order traverse and link binding.

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

var prev: TreeNode? = null

// O(n) time | O(n) space
fun flatten(node: TreeNode?) {
   if (node == null) return
   flatten(node.right)
   flatten(node.left)
   node.right = prev
   node.left = null
   prev = node
}
```
