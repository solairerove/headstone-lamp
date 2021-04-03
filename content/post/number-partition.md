---
title: "Number Partition"
date: 2021-03-04T18:55:57+03:00
draft: true
categories: ["greedy"]
---

[Формулировка задачи](https://neerc.ifmo.ru/wiki/index.php?title=%D0%9D%D0%B0%D1%85%D0%BE%D0%B6%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BA%D0%BE%D0%BB%D0%B8%D1%87%D0%B5%D1%81%D1%82%D0%B2%D0%B0_%D1%80%D0%B0%D0%B7%D0%B1%D0%B8%D0%B5%D0%BD%D0%B8%D0%B9_%D1%87%D0%B8%D1%81%D0%BB%D0%B0_%D0%BD%D0%B0_%D1%81%D0%BB%D0%B0%D0%B3%D0%B0%D0%B5%D0%BC%D1%8B%D0%B5)

[number partition](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/NumberPartition.kt)

```kotlin
fun main() {
    var n = 6

    val res = mutableListOf<Int>()
    for (i in 1..n) {
        if (n - i >= i + 1) {
            res.add(i)
        } else {
            res.add(n)
            break
        }
        n -= i
    }

    print("${res.size}\n")
    res.forEach { print("$it ") }
}
```
