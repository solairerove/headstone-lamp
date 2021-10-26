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

Make recursive swap traversal.

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

// O(n) space | O(log(n))
fun maxPathSum(node: TreeNode?): Int {
    val (_, maxSumArray) = findMaxSum(node)
    return maxSumArray
}

fun findMaxSum(node: TreeNode?): List<Int> {
    if (node == null) return listOf(0, Int.MIN_VALUE)

    val (left, leftPathSum) = findMaxSum(node.left)
    val (right, rightPathSum) = findMaxSum(node.right)
    val maxLeafSum = max(left, right)

    val maxBranch = max(maxLeafSum + node.value, node.value)
    val maxRoot = max(left + node.value + right, maxBranch)
    val maxPathSum = listOf(leftPathSum, rightPathSum, maxRoot).max()!!

    return listOf(maxBranch, maxPathSum)
}
```
