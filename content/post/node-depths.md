---
title: "Node Depths"
date: 2021-10-26T15:50:17+03:00
draft: true
categories: ["binary tree"]
---

Find sum of nodes depths. Depth is distance between root and node.

         3
       /   \
      7     8
     / \   / \
    14 15 21 25


Output: 10

[node depths](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/NodeDepths.kt) \
[easy leetcode version](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Make tree traversal, increment depth on recursive call.

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

// O(n) time | O(h) space
// n - number of nodes
// h - height of tree
fun nodeDepths(node: TreeNode?, depth: Int = 0): Int {
    if (node == null) return 0

    return depth + nodeDepths(node.left, depth + 1) + nodeDepths(node.right, depth + 1)
}
```
