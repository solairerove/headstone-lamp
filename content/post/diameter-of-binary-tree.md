---
title: "Diameter of Binary Tree"
date: 2021-10-27T12:00:34+03:00
draft: true
categories: ["binary tree"]
---

Given the root of a binary tree, return the length of the diameter of the tree. \
The diameter of a binary tree is the length of the longest path between any two nodes in a tree.\
This path may or may not pass through the root.\
The length of a path between two nodes is represented by the number of edges between them.

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: 3

[diameter of binary tree](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/DiameterOfBinaryTree.kt) \
[leetcode](https://leetcode.com/problems/diameter-of-binary-tree/)

No clue

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

data class TreeInfo(val diameter: Int, val height: Int)

// O(n) time | O(h) space
fun binaryTreeDiameter(node: TreeNode?): Int {
    return getTreeInfo(node).diameter
}

fun getTreeInfo(node: TreeNode?): TreeInfo {
    if (node == null) return TreeInfo(diameter = 0, height = 0)

    val left = getTreeInfo(node.left)
    val right = getTreeInfo(node.right)

    val longestHeight = left.height + right.height
    val maxDiameter = max(left.diameter, right.diameter)
    val currDiameter = max(longestHeight, maxDiameter)
    val currHeight = 1 + max(left.height, right.height)

    return TreeInfo(diameter = currDiameter, height = currHeight)
}
```
