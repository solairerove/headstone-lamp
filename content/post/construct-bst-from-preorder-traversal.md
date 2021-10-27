---
title: "Construct Bst From Preorder Traversal"
date: 2021-10-27T17:33:24+03:00
draft: true
categories: ["binary search tree"]
---

Output:

        14
       /  \
      7   21
     /\   /\
    3  8 15 25

Input: [14, 7, 3, 8, 21, 15, 25]

[construct bst from preorder traversal](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/ConstructBSTFromPreorderTraversal.kt) \
[leetcode](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

private var i = 0

// O(n) time | O(n) space
fun bstFromPreorder(preorder: List<Int>): BSTNode? {
    return constructBST(preorder)
}

fun constructBST(preorder: List<Int>, bound: Int = Int.MAX_VALUE): BSTNode? {
    if (i == preorder.size || preorder[i] > bound) return null
    val root = BSTNode(value = preorder[i++])
    root.left = constructBST(preorder, root.value)
    root.right = constructBST(preorder, bound)
    return root
}
```
