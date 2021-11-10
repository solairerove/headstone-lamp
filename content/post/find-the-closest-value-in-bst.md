---
title: "Find the Closest Value in Bst"
date: 2021-10-22T14:30:19+03:00
draft: true
categories: ["binary search tree"]
---

        14
       /  \
      7   21
     /\   /\
    3  8 15 25

Input: 16 \
Output: 15

[find the closest value](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/FIndTheClosestValue.kt) \
[leetcode](https://leetcode.com/problems/closest-binary-search-tree-value/)

Iterate through tree. Find the closest value to target. \
The closest is the smallest delta result, \
so it can be represented as `abs(target - value) < abs(target - closest)` 

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

// O(log(n)) time | O(1) space
// worst O(n) time | O(1) space if bst has one branch
fun findTheClosestValueInBst(tree: BSTNode?, target: Int): Int {
    var closest = tree!!.value
    var node = tree

    inner@ while (node != null) {
        if (abs(target - node.value) < abs(target - closest)) closest = node.value

        node = when {
            target < node.value -> node.left
            target > node.value -> node.right
            else -> break@inner
        }
    }

    return closest
}
```
