---
title: "Traverse Bst"
date: 2021-10-25T13:53:31+03:00
draft: true
categories: ["binary search tree"]
---

        14
       /  \
      7   21
     /\   /\
    3  8 15 25

Output: \
in order: [3, 7, 8, 14, 15, 21, 25]
pre order: [14, 7, 3, 8, 21, 15, 25]
post order: [3, 8, 7, 15, 25, 21, 14]

[traverse bst](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/TraverseBST.kt)

No clue why 

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

// O(n) time | O(n) space
fun inOrderTraversal(node: BSTNode?, arr: MutableList<Int>): List<Int> {
    if (node != null) {
        inOrderTraversal(node.left, arr)
        arr.add(node.value)
        inOrderTraversal(node.right, arr)
    }
    return arr
}

// O(n) time | O(n) space
fun preOrderTraversal(node: BSTNode?, arr: MutableList<Int>): List<Int> {
    if (node != null) {
        arr.add(node.value)
        preOrderTraversal(node.left, arr)
        preOrderTraversal(node.right, arr)
    }
    return arr
}

// O(n) time | O(n) space
fun postOrderTraversal(node: BSTNode?, arr: MutableList<Int>): List<Int> {
    if (node != null) {
        postOrderTraversal(node.left, arr)
        postOrderTraversal(node.right, arr)
        arr.add(node.value)
    }
    return arr
}
```
