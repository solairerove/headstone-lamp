---
title: "Permutations"
date: 2021-06-04T18:46:38+03:00
draft: true
categories: ["recursion"]
---

Input: [1, 2] \
Output: [[1, 2], [2, 1]]

[permutations](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/recursion/Permutations.kt)

```kotlin
// O(n*n!) time | O(n*n!) space
fun permutations(arr: List<Int>): List<List<Int>> {
    val perms = mutableListOf<List<Int>>()
    permutations(arr.toMutableList(), 0, perms)

    return perms
}

fun permutations(arr: MutableList<Int>, i: Int, perms: MutableList<List<Int>>) {
    val n = arr.size
    if (i == n - 1) {
        perms.add(arr.toList())
        return
    }

    for (j in i until n) {
        swap(arr, i, j)
        permutations(arr, i + 1, perms)
        swap(arr, i, j)
    }
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val tmp = arr[i]
    arr[i] = arr[j]
    arr[j] = tmp
}
```
