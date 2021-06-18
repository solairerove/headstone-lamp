---
title: "Largest Range"
date: 2021-06-18T15:18:35+03:00
draft: true
categories: ["arrays"]
---

Input: [1, 9, 10, 12, 14, 16, 11, 17, 13, 3] \
Output: [9, 14]

[largest range](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/LargestRange.kt)

```kotlin
// O(n) time | O(n) space
fun largestRange(arr: List<Int>): List<Int> {
    var range = listOf(arr[0], arr[0])
    var length = 0
    val nums = mutableMapOf<Int, Boolean>()
    arr.forEach { nums[it] = true }

    for (el in arr) {
        if (nums[el] == false) continue
        nums[el] = false
        var currLength = 1
        var low = el - 1
        var high = el + 1

        while (low in nums) {
            nums[low] = false
            currLength++
            low--
        }

        while (high in nums) {
            nums[high] = false
            currLength++
            high++
        }

        if (currLength > length) {
            length = currLength
            range = listOf(low + 1, high - 1)
        }
    }

    return range
}
```
