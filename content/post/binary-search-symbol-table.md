---
title: "Binary Search Symbol Table"
date: 2021-11-02T14:42:40+03:00
draft: true
categories: ["symbol table"]
---

Упорядоченная символьная таблица для бинарного поиска.

[binary search st](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/symbol_table/BinarySearchST.kt)

```kotlin
private const val INITIAL_CAPACITY = 2

class BinarySearchST<Key : Comparable<Key>, Value> {

    private var keys: MutableList<Key?>
    private var vals: MutableList<Value?>
    private var n: Int = 0

    constructor() : this(INITIAL_CAPACITY)

    constructor(capacity: Int) {
        keys = MutableList(capacity) { null }
        vals = MutableList(capacity) { null }
    }

    fun size() = n

    fun delete(key: Key) = put(key, null)

    fun isEmpty(): Boolean = size() == 0

    fun contains(key: Key): Boolean = get(key) == null

    fun put(key: Key, value: Value?) {
        val i = rank(key)
        if (i < size() && keys[i]?.compareTo(key) == 0) {
            vals[i] = value
            return
        }


        for (j in size() downTo i + 1) {
            keys[j] = keys[j - 1]
            vals[j] = vals[j - 1]
        }

        keys[i] = key
        vals[i] = value
        n++
    }

    fun get(key: Key): Value? {
        if (isEmpty()) return null

        val i = rank(key)
        return if (i < size() && keys[i]?.compareTo(key) == 0) vals[i]
        else null
    }

    private fun rank(key: Key): Int {
        var low = 0
        var high = size() - 1

        while (low <= high) {
            val mid = low + (high - low) / 2
            val cmp = key.compareTo(keys[mid]!!)
            when {
                cmp < 0 -> high = mid - 1
                cmp > 0 -> low = mid + 1
                else -> return mid
            }
        }

        return low
    }

    fun min(): Key {
        if (isEmpty()) throw NoSuchElementException("called min() with empty symbol table")
        return keys[0]!!
    }

    fun max(): Key {
        if (isEmpty()) throw NoSuchElementException("called max() with empty symbol table")
        return keys[n - 1]!!
    }

    fun keys(): Iterable<Key> {
        return keys(min(), max())
    }

    fun keys(low: Key?, high: Key?): Iterable<Key> {
        if (low == null) throw IllegalArgumentException("first arg to keys() is null")
        if (high == null) throw IllegalArgumentException("second arg to keys() is null")

        val queue = LinkedList<Key>()
        if (low > high) return queue
        for (i in rank(low)..rank(high)) {
            queue.add(keys[i]!!)
        }
        if (contains(high)) queue.add(keys[rank(high)]!!)
        return queue
    }
}
```
