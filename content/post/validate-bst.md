---
title: "Validate BST"
date: 2021-10-25T13:29:01+03:00
draft: true
categories: ["binary search tree"]
---

        14
       /  \
      7   21
     /\   /\
    3  8 15 25

Output: true

[validate bst](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/ValidateBST.kt) \
[https://algs4.cs.princeton.edu/32bst/BST.java.html#isBST](https://algs4.cs.princeton.edu/32bst/BST.java.html)

Recursive version of `isBST` method. \
BST is valid:
 - if value greater to every left node values
 - if value less than every right node values

So for recursive solution is possible to make expression where
 - max value is current node value for left branches
 - min value is current node value for right branches

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

// O(n) time | O(d) space
fun validateBST(tree: BSTNode): Boolean {
    return isBST(node = tree, min = Int.MIN_VALUE, max = Int.MAX_VALUE)
}

fun isBST(node: BSTNode?, min: Int?, max: Int?): Boolean {
    if (node == null) return true
    if (min != null && node.value < min) return false
    if (max != null && node.value >= max) return false
    return isBST(node.left, min, node.value) && isBST(node.right, node.value, max)
}
```
