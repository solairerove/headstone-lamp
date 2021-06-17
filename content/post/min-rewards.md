---
title: "Min Rewards"
date: 2021-06-17T19:07:12+03:00
draft: true
categories: ["arrays"]
---

Input: [9, 2, 3, 1, 8, 4, 7] \
Output: 11

[min rewards](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/MinRewards.kt)

```kotlin
// O(n) time | O(n) space
fun minRewards(scores: List<Int>): Int {
    val n = scores.size
    val rewards = MutableList(n) { 1 }

    for (i in 1 until n) {
        if (scores[i] > scores[i - 1]) {
            rewards[i] = rewards[i - 1] + 1
        }
    }

    for (i in n - 2 downTo 0) {
        if (scores[i] > scores[i + 1]) {
            rewards[i] = max(rewards[i], rewards[i + 1] + 1)
        }
    }

    return rewards.sum()
}
```
