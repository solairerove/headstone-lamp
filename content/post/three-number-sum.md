---
title: "Three Number Sum"
date: 2021-04-29T15:13:22+03:00
draft: true
categories: ["arrays"]
---

Input: arr = [-9, -7, -6, -4, 0, 2, 3, 4, 5, 7], target = -1 \
Output: [[-9, 3, 5], [-7, 2, 4], [-6, 0, 5], [-6, 2, 3], [-4, 0, 3]]

[three number sum](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/ThreeNumberSum.kt)

```kotlin
// O(n^2) time | O(n) space
fun threeNumberSum(arr: MutableList<Int>, target: Int): List<List<Int>> {
    arr.sort()

    val triplets = mutableListOf<MutableList<Int>>()

    for (i in 0 until arr.size - 2) {
        var low = i + 1
        var high = arr.size - 1

        while (low < high) {
            val curr = arr[i] + arr[low] + arr[high]

            when {
                curr == target -> {
                    triplets.add(mutableListOf(arr[i], arr[low], arr[high]))
                    low++
                    high--
                }
                curr < target -> low++
                else -> high--
            }
        }
    }

    return triplets
}
```
