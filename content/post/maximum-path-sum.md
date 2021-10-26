---
title: "Maximum Path Sum"
date: 2021-10-26T18:25:00+03:00
draft: true
categories: ["binary tree"]
---

         3
       /   \
      7     8
     / \   / \
    14 15 21 25

Output: 58 (15 + 7 + 3 + 8 + 25)

[max path sum](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/MaximumPathSum.kt) \
[leetcode](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

A path from start to end, goes up on the tree for 0 or more steps, \
then goes down for 0 or more steps. Once it goes down, it can't go up. \
Each path has a highest node, which is also the lowest common ancestor of all other nodes on the path.\
A recursive method maxPathDown(TreeNode node) (1) computes the maximum path sum with highest node is the input node,\
update maximum if necessary (2) returns the maximum sum of the path that can be extended to input node's parent.

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

var maxValue = 0

// O(n) space | O(log(n))
fun maxPathSum(node: TreeNode?): Int {
    maxValue = Int.MIN_VALUE
    maxPathDown(node)
    return maxValue
}

fun maxPathDown(node: TreeNode?): Int {
    if (node == null) return 0
    val left = max(0, maxPathDown(node.left))
    val right = max(0, maxPathDown(node.right))
    maxValue = max(maxValue, left + right + node.value)
    return max(left, right) + node.value
}
```
