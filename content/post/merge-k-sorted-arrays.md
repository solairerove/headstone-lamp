---
title: "Merge K Sorted Arrays"
date: 2021-04-20T22:30:02+03:00
draft: true
categories: ["heap"]
---

Input: lists = [[1,4,5],[1,3,4],[2,6]] \
Output: [1,1,2,3,4,4,5,6]

[leetcode](https://leetcode.com/problems/merge-k-sorted-lists/)

[merge k sorted arrays](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/heap/MergeKSortedArrays.kt)

```kotlin
// O(nlog(k) + k) time | O(n + k) space
// n - total elements, k - number of arrays
fun mergeKSortedArrays(arrays: List<List<Int>>): List<Int> {
    val res = mutableListOf<Int>()
    val min = mutableListOf<Element>()
    for (i in arrays.indices) {
        min.add(Element(i, 0, arrays[i][0]))
    }

    val minHeap = Heap(min)
    while (minHeap.size() != 0) {
        val (arrIdx, idx, el) = minHeap.remove()
        res.add(el)
        if (idx < arrays[arrIdx].size - 1) {
            minHeap.insert(Element(arrIdx, idx + 1, arrays[arrIdx][idx + 1]))
        }
    }

    return res
}

data class Element(val arrIdx: Int, val idx: Int, val el: Int)

class Heap(arr: MutableList<Element>) {
    private val heap: MutableList<Element> = arr

    init {
        val n = arr.size
        for (k in n / 2 downTo 0) {
            sink(arr, k, n - 1)
        }
    }

    private fun sink(arr: MutableList<Element>, curr: Int, n: Int) {
        var k = curr
        while (2 * k + 1 <= n) {
            var j = 2 * k + 1
            if (j < n && less(arr, j, j + 1)) j++
            if (!less(arr, k, j)) break
            swap(arr, k, j)
            k = j
        }
    }

    private fun swim(arr: MutableList<Element>, curr: Int) {
        var k = curr
        while (k > 0 && less(arr, (k - 1) / 2, k)) {
            swap(arr, (k - 1) / 2, k)
            k = (k - 1) / 2
        }
    }

    fun size(): Int = heap.size

    fun remove(): Element {
        swap(heap, 0, heap.size - 1)
        val toRemove = heap.removeAt(heap.size - 1)
        sink(heap, 0, heap.size - 1)

        return toRemove
    }

    fun insert(value: Element) {
        heap.add(value)
        swim(heap, heap.size - 1)
    }

    private fun less(arr: MutableList<Element>, i: Int, j: Int): Boolean {
        return arr[i].el > arr[j].el
    }

    private fun swap(arr: MutableList<Element>, i: Int, j: Int) {
        val temp = arr[i]
        arr[i] = arr[j]
        arr[j] = temp
    }
}
```
