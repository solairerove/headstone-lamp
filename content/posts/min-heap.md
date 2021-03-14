---
title: "Min Heap"
date: 2021-03-11T20:27:42+03:00
draft: true
---

Main methods:
- build heap
- sift down
- sift up
- insert
- remove

Node:
- current node -> i
- child one -> (2 * i) + 1
- child two -> (2 * i) + 2
- parent node -> (i - 1) / 2

Transform array to heap (heapify)
- foreach parent sink

[min heap](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/heap/MinHeap.kt) \
[Priority Queues](https://algs4.cs.princeton.edu/24pq/) \
[stepik max heap](https://gist.github.com/solairerove/d1c50a0a88f72cab215e0955a27797dd)

```kotlin
class MinHeap(arr: MutableList<Int>) {

    private val heap = buildHeap(arr)

    // O(1) time | O(1) space
    fun peek(): Int {
        return heap[0]
    }

    // O(log(n)) time | O(1) space
    fun remove(): Int {
        swap(heap, 0, heap.size - 1)
        val min = heap.removeAt(heap.size - 1)
        sink(heap, 0, heap.size - 1)

        return min
    }

    // O(log(n)) time | O(1) space
    fun insert(value: Int) {
        heap.add(value)
        swim(heap, heap.size - 1)
    }

    // O(n) time | O(1) space
    private fun buildHeap(arr: MutableList<Int>): MutableList<Int> {
        val parentIdx = (arr.size - 2) / 2
        for (k in parentIdx downTo 0) {
            sink(arr, k, arr.size - 1)
        }

        return arr
    }

    // O(log(n)) time | O(1) space
    private fun sink(arr: MutableList<Int>, k: Int, n: Int) {
        var idx = k
        while (idx * 2 + 1 <= n) {
            var j = idx * 2 + 1
            if (j < n && less(arr, j, j + 1)) j++
            if (!less(arr, idx, j)) break
            swap(arr, idx, j)
            idx = j
        }
    }

    // O(log(n)) time | O(1) space
    private fun swim(arr: MutableList<Int>, k: Int) {
        var idx = k
        while (idx > 0 && less(arr, (idx - 1) / 2, idx)) {
            swap(arr, (idx - 1) / 2, idx)
            idx = (idx - 1) / 2
        }
    }

    private fun less(arr: MutableList<Int>, i: Int, j: Int): Boolean {
        return arr[i] > arr[j]
    }

    private fun swap(arr: MutableList<Int>, i: Int, j: Int) {
        val temp = arr[i]
        arr[i] = arr[j]
        arr[j] = temp
    }
}
```
