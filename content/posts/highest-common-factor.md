---
title: "Highest Common Factor"
date: 2021-03-02T13:27:30+03:00
draft: true
---

Рекурсивный вариант алгоритма Евклида для нахождения наибольшего общего делителя.

[gcd](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/recursion/HighestCommonFactor.kt)

```kotlin
fun gcd(p: Int, q: Int): Int {
    if (q == 0) {
        return p
    }

    val r = p % q
    return gcd(q, r)
}
```
