---
title: "Sum of Node Depths"
date: 2021-10-29T16:28:14+03:00
draft: true
categories: ["binary tree"]
---


         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: 14

[sum of node depths](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/SumOfNodeDepths.kt)

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

// O(n) time | O(h) space
fun sumOfNodeDepths(node: TreeNode?, depth: Int = 0): Int {
    if (node == null) return 0

    val depthSum = (depth * (depth + 1)) / 2
    return depthSum + sumOfNodeDepths(node.left, depth + 1) + sumOfNodeDepths(node.right, depth + 1)
}
```
