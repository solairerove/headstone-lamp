---
title: "Lru Cache With Capacity"
date: 2021-05-31T19:43:41+03:00
draft: true
categories: ["map"]
---

[lru cache with capacity](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/map/LRUCacheWithCapacity.kt)

```kotlin
open class LRUCacheWithCapacity<K, V>(
    private val capacity: Int,
    loadFactor: Float = 0.75F,
    accessOrder: Boolean = true
) : LinkedHashMap<K, V>(
    capacity,
    loadFactor,
    accessOrder
) {
    override fun removeEldestEntry(eldest: MutableMap.MutableEntry<K, V>?): Boolean {
        return this.size > capacity
    }
}
```
