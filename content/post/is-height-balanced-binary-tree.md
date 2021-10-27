---
title: "Is Height Balanced Binary Tree"
date: 2021-10-27T14:08:59+03:00
draft: true
categories: ["binary tree"]
---

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:
    
    a binary tree in which the left and right subtrees of every node differ in height by no more than 1.
___

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: true

[is height balanced](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/IsHeightBalancedBinaryTree.kt) \
[leetcode](https://leetcode.com/problems/balanced-binary-tree/)

No clue

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

data class IsBalancedTreeInfo(val isBalanced: Boolean, val height: Int)

// O(n) time | O(h) space
fun isBalanced(node: TreeNode?): Boolean {
    return getTreeInfo(node).isBalanced
}

fun getTreeInfo(node: TreeNode?): IsBalancedTreeInfo {
    if (node == null) return IsBalancedTreeInfo(isBalanced = true, height = -1)

    val left = getTreeInfo(node.left)
    val right = getTreeInfo(node.right)

    val isBalanced = left.isBalanced && right.isBalanced
            && abs(left.height - right.height) <= 1

    val height = max(left.height, right.height) + 1
    return IsBalancedTreeInfo(isBalanced, height)
}
```
