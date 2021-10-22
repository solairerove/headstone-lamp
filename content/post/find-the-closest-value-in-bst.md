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

[find the closest value](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/FIndTheClosestValue.kt)

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

// O(log(n)) time | O(1) space
// worst O(n) time | O(1) space
fun findTheClosestValueInBst(tree: BST, target: Int): Int {
    return findTheClosestValueInBst(tree, target, tree.value)
}

fun findTheClosestValueInBst(tree: BST?, target: Int, closest: Int): Int {
    var newClosest = closest
    var currNode = tree
    inner@ while (currNode != null) {
        if (abs(target - newClosest) > abs(target - currNode.value)) {
            newClosest = currNode.value
        }

        currNode = when {
            target < currNode.value -> currNode.left
            target > currNode.value -> currNode.right
            else -> break@inner
        }
    }

    return newClosest
}
```
