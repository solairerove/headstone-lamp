---
title: "Same Bst"
date: 2021-11-08T13:04:06+03:00
draft: true
categories: ["binary search tree"]
---

Input: [1, 2, 3] [1, 2, 3]
Output: true

[same bsts](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/SameBSTs.kt)

```kotlin
// O(nˆ2) time | O(d) space
// n is number of nodes
// d is depth
fun sameBsts(
        arrOne: List<Int>,
        arrTwo: List<Int>,
        idxOne: Int = 0,
        idxTwo: Int = 0,
        min: Int = Int.MIN_VALUE,
        max: Int = Int.MAX_VALUE
): Boolean {
    if (idxOne == -1 || idxTwo == -1) return idxOne == idxTwo
    if (arrOne[idxOne] != arrTwo[idxTwo]) return false

    val smallOne = getSmall(arrOne, idxOne, min)
    val smallTwo = getSmall(arrTwo, idxTwo, min)
    val bigOne = getBig(arrOne, idxOne, max)
    val bigTwo = getBig(arrTwo, idxTwo, max)

    val curr = arrOne[idxOne]
    val left = sameBsts(arrOne, arrTwo, smallOne, smallTwo, min, curr)
    val right = sameBsts(arrOne, arrTwo, bigOne, bigTwo, curr, max)

    return left && right
}

fun getSmall(arr: List<Int>, idx: Int, min: Int): Int {
    for (i in idx + 1 until arr.size) {
        if (arr[i] < arr[idx] && arr[i] >= min) {
            return i
        }
    }
    return -1
}

fun getBig(arr: List<Int>, idx: Int, max: Int): Int {
    for (i in idx + 1 until arr.size) {
        if (arr[i] >= arr[idx] && arr[i] < max) {
            return i
        }
    }
    return -1
}
```
