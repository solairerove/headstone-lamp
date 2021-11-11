---
title: "Convert Sorted Array to BST"
date: 2021-11-06T13:06:30+03:00
draft: true
categories: ["binary search tree"]
---

Output:

        0
       / \
      -3  9
     /    /
    -10  5 

Input: [-10, -3, 0, 5, 9]

[convert sorted array to bst](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/ConvertSortedArrayToBST.kt)
[leetcode](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

```kotlin
open class BST(var value: Int) {
    var left: BST? = null
    var right: BST? = null
}

// O(n) time | O(n) space
fun sortedArrayToBST(arr: IntArray, low: Int = 0, high: Int = arr.size - 1): BSTNode? {
    if (high < low) return null

    val mid = low + (high - low) / 2
    val bst = BSTNode(arr[mid])
    bst.left = sortedArrayToBST(arr, low, mid - 1)
    bst.right = sortedArrayToBST(arr, mid + 1, high)
    return bst
}
```
