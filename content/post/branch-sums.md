---
title: "Branch Sums"
date: 2021-10-26T12:11:17+03:00
draft: true
categories: ["binary tree"]
---

         3
       /   \
      7     8
     / \   / \
    14 15 21 25


Output: [24, 25, 32, 36]

[branch sums](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/BranchSums.kt) \
[easy leetcode version](https://leetcode.com/problems/path-sum/)

Make pre order tree traversal, summarize current value. \ 
If there's no left or right, we're done with branch.

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

// O(n) time | O(n) space
fun branchSums(node: TreeNode): List<Int> {
    val sums = mutableListOf<Int>()
    calculate(node, 0, sums)

    return sums
}

fun calculate(node: TreeNode?, sum: Int, sums: MutableList<Int>) {
    if (node == null) return

    val currSum = sum + node.value
    if (node.left == null && node.right == null) {
        sums.add(currSum)
        return
    }

    calculate(node.left, currSum, sums)
    calculate(node.right, currSum, sums)
}
```
