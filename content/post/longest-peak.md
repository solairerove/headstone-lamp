---
title: "Longest Peak"
date: 2021-05-04T13:03:22+03:00
draft: true
categories: ["arrays"]
---

Input: arr = [3, -4, 7, 12, 4, 20, 15, 6, -2, 5, 16, 11, 1]\
Output: 5

[longest peak](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/LongestPeak.kt)

```kotlin
// O(n) time | O(1) space
fun longestPeak(arr: List<Int>): Int {
    var longestPeakLen = 0
    var i = 1

    while (i < arr.size - 1) {
        val isPeak = arr[i] > arr[i - 1] && arr[i] > arr[i + 1]

        if (!isPeak) {
            i++
            continue
        }

        var low = i - 2
        while (low >= 0 && arr[low] < arr[low + 1]) low--

        var high = i + 2
        while (high < arr.size && arr[high] < arr[high - 1]) high++

        val currPeakLen = high - low - 1
        longestPeakLen = max(longestPeakLen, currPeakLen)
        i = high
    }

    return longestPeakLen
}
```
