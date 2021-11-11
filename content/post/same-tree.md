---
title: "Same Tree"
date: 2021-11-11T15:54:19+03:00
draft: true
categories: ["binary tree"]
---

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

[same tree](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_tree/SameTree.kt) \
[leetcode](https://leetcode.com/problems/same-tree/)

```kotlin
class TreeNode(var value: Int) {
    var left: TreeNode? = null
    var right: TreeNode? = null
}

// O(n) time | O(n) space
fun isSameTree(p: TreeNode?, q: TreeNode?): Boolean {
    if (p == null && q == null) return true
    if (p == null || q == null) return false
    if (p.value != q.value) return false
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right)
}
```
