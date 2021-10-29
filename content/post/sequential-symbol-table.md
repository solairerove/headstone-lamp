---
title: "Sequential Symbol Table"
date: 2021-10-29T17:46:36+03:00
draft: true
categories: ["symbol table"]
---

Символьная таблица для последовательного поиска в неупорядоченном массиве.

[sequential st](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/symbol_table/SequentialSearchST.kt)

```kotlin
class SequentialSearchST<Key, Value> {
    private var first: Node? = null

    inner class Node(val key: Key, var value: Value?, val next: Node?)

    fun get(key: Key): Value? {
        var x = first
        while (x != null) {
            if (key?.equals(x.key) == true) {
                return x.value
            }
            x = x.next
        }

        return null
    }

    fun put(key: Key, value: Value?) {
        var x = first
        while (x != null) {
            if (key?.equals(x.key) == true) {
                x.value = value
                return
            }
            x = x.next
        }
        first = Node(key, value, first)
    }
}
```
