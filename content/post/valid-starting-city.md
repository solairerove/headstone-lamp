---
title: "Valid Starting City"
date: 2021-04-27T22:30:10+03:00
draft: true
categories: ["greedy"]
---

Input: distances = [10, 15, 10, 25, 5], fuel = [1, 2, 3, 1, 2], mpg = 5 \
Output: 4

[valid starting city](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/ValidStartingCity.kt) \
type of [leetcode destination-city](https://leetcode.com/problems/destination-city/)

```kotlin
// O(n) time | O(1) space
fun validStartingCity(distances: List<Int>, fuel: List<Int>, mpg: Int): Int {
    var currMiles = 0
    var idx = 0
    var totalMiles = 0

    for (i in 1 until distances.size) {
        val prevDistance = distances[i - 1]
        val prevFuel = fuel[i - 1]
        currMiles += prevFuel * mpg - prevDistance

        if (currMiles < totalMiles) {
            idx = i
            totalMiles = currMiles
        }
    }

    return idx
}
```
