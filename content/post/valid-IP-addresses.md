---
title: "Valid IP Addresses"
date: 2021-05-24T20:36:15+03:00
draft: true
categories: ["strings"]
---

Input: "19216801" \
Output: [19.216.80.1, 192.16.80.1, 192.168.0.1]

[valid ip addresses](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/ValidIPAddresses.kt)

```kotlin
import kotlin.math.min

// O(1) time | O(1) space
fun validIPAddresses(s: String): List<String> {
    val n = s.length
    val addresses = mutableListOf<String>()

    for (i in 1 until min(n, 4)) {
        val parts = mutableListOf("", "", "", "")

        parts[0] = s.substring(0, i)
        if (!isValidPart(parts[0])) continue

        for (j in i + 1 until i + min(n - i, 4)) {
            parts[1] = s.substring(i, j)
            if (!isValidPart(parts[1])) continue

            for (k in j + 1 until j + min(n - j, 4)) {
                parts[2] = s.substring(j, k)
                parts[3] = s.substring(k)

                if (isValidPart(parts[2]) && isValidPart(parts[3])) {
                    addresses.add(parts.joinToString("."))
                }
            }
        }
    }

    return addresses
}

fun isValidPart(s: String): Boolean {
    val asInt = s.toInt()
    if (asInt > 255) return false

    return s.length == asInt.toString().length
}
```
