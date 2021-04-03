---
title: "Knapsack Problem"
date: 2021-03-04T17:58:03+03:00
draft: true
categories: ["greedy"]
---

[Формулировка задачи](https://neerc.ifmo.ru/wiki/index.php?title=%D0%97%D0%B0%D0%B4%D0%B0%D1%87%D0%B0_%D0%BE_%D1%80%D1%8E%D0%BA%D0%B7%D0%B0%D0%BA%D0%B5)

[knapsack problem](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/KnapsackProblem.kt)

```kotlin
import java.text.DecimalFormat

fun main() {
    var backPackSize = 50

    val items = mutableListOf(
        Item(worth = 60, volume = 20, worthPerVolume = (60 / 20).toDouble()),
        Item(worth = 100, volume = 50, worthPerVolume = (100 / 50).toDouble()),
        Item(worth = 120, volume = 30, worthPerVolume = (120 / 30).toDouble())
    )

    items.sortByDescending { it.worthPerVolume }

    var res = 0.0
    for (item in items) {
        if (item.volume < backPackSize) {
            res += item.worth
            backPackSize -= item.volume
        } else {
            res += (backPackSize / item.volume).toDouble() * item.worth.toDouble()
            break
        }
    }

    val df = DecimalFormat("#####0.000")
    print(df.format(res))
}

data class Item(
    val worth: Int,
    val volume: Int,
    val worthPerVolume: Double
)
```
