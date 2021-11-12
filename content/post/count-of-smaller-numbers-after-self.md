---
title: "Count of Smaller Numbers After Self"
date: 2021-11-12T14:31:57+03:00
draft: true
categories: ["binary search tree"]
---

You are given an integer array nums and you have to return a new counts array. \
The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

Input: [5, 2, 6, 1]
Output: [2, 1, 1, 0]

[count of smaller numbers after self](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/binary_search_tree/CountOfSmallerNumbersAfterSelf.kt)
[leetcode](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)
[solution](https://leetcode.com/problems/count-of-smaller-numbers-after-self/discuss/445769/merge-sort-CLEAR-simple-EXPLANATION-with-EXAMPLES-O(n-lg-n))

```kotlin
data class ArrayValWithOrigIdx(val value: Int, val originalIdx: Int)

// O(log(n)) time | O(n) space
fun countSmaller(arr: IntArray?): List<Int> {
    if (arr == null || arr.isEmpty()) return emptyList()
    val n = arr.size
    val res = IntArray(n)

    val newNums = Array(n) { ArrayValWithOrigIdx(0, 0) }
    for (i in 0 until n) {
        newNums[i] = ArrayValWithOrigIdx(arr[i], i)
    }

    mergeSortAndCount(newNums, 0, n - 1, res)

    val resList = LinkedList<Int>()
    for (i in res) {
        resList.add(i)
    }

    return resList
}

fun mergeSortAndCount(
    arr: Array<ArrayValWithOrigIdx>,
    low: Int,
    high: Int,
    res: IntArray
) {
    if (low >= high) return

    val mid = low + (high - low) / 2
    mergeSortAndCount(arr, low, mid, res)
    mergeSortAndCount(arr, mid + 1, high, res)

    var i = low
    var j = mid + 1
    val merged = LinkedList<ArrayValWithOrigIdx>()
    var numElementRightArrayLessThanLeftArray = 0
    while (i < mid + 1 && j <= high) {
        if (arr[i].value > arr[j].value) {
            ++numElementRightArrayLessThanLeftArray
            merged.add(arr[j])
            ++j
        } else {
            res[arr[i].originalIdx] += numElementRightArrayLessThanLeftArray
            merged.add(arr[i])
            ++i
        }
    }

    while (i < mid + 1) {
        res[arr[i].originalIdx] += numElementRightArrayLessThanLeftArray
        merged.add(arr[i])
        ++i
    }

    while (j <= high) {
        merged.add(arr[j])
        ++j
    }

    var pos = low
    for (m in merged) {
        arr[pos] = m
        ++pos
    }
}
```
