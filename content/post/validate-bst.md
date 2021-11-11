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
[leetcode](https://leetcode.com/problems/validate-binary-search-tree/)

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
fun isBST(root: BSTNode?, min: Int? = null, max: Int? = null): Boolean {
    if (root == null) return true
    if (min != null && root.value <= min) return false
    if (max != null && root.value >= max) return false

    return isBST(root.left, min, root.value) && isBST(root.right, root.value, max)
}
```
