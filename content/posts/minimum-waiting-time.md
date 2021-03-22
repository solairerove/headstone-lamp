---
title: "Minimum Waiting Time"
date: 2021-03-08T17:27:29+03:00
draft: true
---

Given non-empty array of positive int, that define time to execute.\
Only one query can be executed at time, but in any order. \
Get minimal waiting time to execute all queries. \
Solid step is ascending sort. \
9 6 5 2 3 1 -> 1 2 3 5 6 9 -> 0 + 1 + (1 + 2) + (1 + 2 + 3) + (1 + 2 + 3 + 5) + (1 + 2 + 3 + 5 + 6) = 38

[minimal waiting time](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/MinimumWaitingTime.kt)

```kotlin
// O(nlogn) time | O(1) space
fun minimumWaitingTime(queries: MutableList<Int>): Int {
    queries.sort()

    var minimumWaitingTime = 0
    var previousSum = queries[0]
    for (i in 1 until queries.size) {
        minimumWaitingTime += previousSum
        previousSum += queries[i]
    }

    return minimumWaitingTime
}
```
