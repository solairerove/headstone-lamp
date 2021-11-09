---
title: "BST"
date: 2021-11-09T12:25:02+03:00
draft: true
categories: ["symbol table"]
---

Дерево бинарного поиска.
Бинарное дерево, в котором каждый узел содержит клю и связанное с ним значение.
Удоавлетворяет условию, что ключ в любом узле больше ключей во всех узлах левого поддерева \
и меньше ключей во всех узлах правого поддерева этого узла.

Методы: \
- `size(): Int` максимально простой, возвращает 0 для нулевой ссылки и `n` для любой ненулевой
- `get(key: Key): Value?` рекурсивный поиск по узлам.
- `put(key: Key, value: Value): Unit` рекурсивный поиск по узлам и перезапись существующего значения \
   или же создание нового узла.
- `min(): Key` переход по левым узлам до упора
- `max(): Key` переход по правым узлам до упора
- `floor(key: Key): Key` нижняя опора. наибольший ключ меньше заданного(по факту наименьший правый узел)
- `ceiling(key: Key): Key` верхняя опора. наименьший ключ больше заданного
- `rank(key: Key): Int` возвращает количество ключей строго меньше заданного \
   основная идея состоит в `cmp > 0 -> rank(key, x.right) + size(x.left) + 1` 
- `select(k: Int): Key` возвращет ключ, ранг которого равен заданному значение \
   основная идеия состоит в `t < k -> select(x.right, k - t - 1)` так как любой узел можно считать корнем поддерева
- `deleteMin(): Unit` проходим по левой стороне, пока не встретим узел с нулевой левой ссылкой. \
   заменяем ссылку на этот узел его правой ссылкой
- `delete(key: Key): Unit` удаление по методу Т. Хиббарда \
   сохраняем ссылку на удаляемый узел \
   заносим минимальный ключ с правого поддерева \
   в правую ссылку удаляем преемника \
   перебиваем левую ссылку
- `print(): Unit` обычный рекурсивный inorder traverse
- `keys(): Iterable<Key>` тоже самое только с учетом диапазона

[bst](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/symbol_table/BST.kt)

```kotlin
class BST<Key : Comparable<Key>, Value> {
   private var root: Node? = null

   inner class Node(var key: Key, value: Value, var n: Int) {
      var value: Value? = value
      var right: Node? = null
      var left: Node? = null
   }

   fun size(): Int = size(x = root)

   private fun size(x: Node?): Int {
      if (x == null) return 0
      return x.n
   }

   fun get(key: Key): Value? = get(x = root, key = key)

   private fun get(x: Node?, key: Key): Value? {
      if (x == null) return null

      val cmp = key.compareTo(x.key)
      return when {
         cmp < 0 -> get(x.left, key)
         cmp > 0 -> get(x.right, key)
         else -> x.value
      }
   }

   fun put(key: Key, value: Value) {
      root = put(x = root, key = key, value = value)
   }

   private fun put(x: Node?, key: Key, value: Value): Node {
      if (x == null) return Node(key = key, value = value, n = 1)

      val cmp = key.compareTo(x.key)
      when {
         cmp < 0 -> x.left = put(x = x.left, key = key, value = value)
         cmp > 0 -> x.right = put(x = x.right, key = key, value = value)
         else -> x.value = value
      }
      x.n = size(x.left) + size(x.right) + 1

      return x
   }

   fun min(): Key = min(root!!).key

   private fun min(x: Node): Node {
      if (x.left == null) return x
      return min(x.left!!)
   }

   fun max(): Key = max(root!!).key

   private fun max(x: Node): Node {
      if (x.right == null) return x
      return max(x.right!!)
   }

   fun floor(key: Key): Key? {
      val x = floor(root, key) ?: return null
      return x.key
   }

   private fun floor(x: Node?, key: Key): Node? {
      if (x == null) return null

      val cmp = key.compareTo(x.key)
      if (cmp == 0) return x
      if (cmp < 0) return floor(x.left, key)

      return floor(x.right, key) ?: x
   }

   fun ceiling(key: Key): Key? {
      val x = ceiling(root, key) ?: return null
      return x.key
   }

   private fun ceiling(x: Node?, key: Key): Node? {
      if (x == null) return null

      val cmp = key.compareTo(x.key)
      if (cmp == 0) return x
      if (cmp < 0) return ceiling(x.left, key) ?: x

      return floor(x.right, key)
   }

   fun rank(key: Key): Int = rank(key, root)

   private fun rank(key: Key, x: Node?): Int {
      if (x == null) return 0

      val cmp = key.compareTo(x.key)
      return when {
         cmp < 0 -> rank(key, x.left)
         cmp > 0 -> rank(key, x.right) + size(x.left) + 1
         else -> return size(x.left)
      }
   }

   fun select(k: Int): Key? = select(root, k)?.key

   private fun select(x: Node?, k: Int): Node? {
      if (x == null) return null

      val t = size(x.left)
      return when {
         t > k -> select(x.left, k)
         t < k -> select(x.right, k - t - 1)
         else -> x
      }
   }

   fun deleteMin() {
      root = deleteMin(root)
   }

   private fun deleteMin(x: Node?): Node? {
      if (x?.left == null) return x?.right
      x.left = deleteMin(x.left)
      x.n = size(x.left) + size(x.right) + 1
      return x
   }

   fun delete(key: Key) {
      root = delete(root, key)
   }

   private fun delete(node: Node?, key: Key): Node? {
      var x = node ?: return null

      val cmp = key.compareTo(x.key)
      when {
         cmp < 0 -> x.left = delete(x.left, key)
         cmp > 0 -> x.right = delete(x.right, key)
         else -> {
            if (x.right == null) return x.left
            if (x.left == null) return x.right

            val t: Node = x
            x = min(t.right!!)!!
            x.right = deleteMin(t.right)
            x.left = t.left
         }
      }
      x.n = size(x.left) + size(x.right) + 1
      return x
   }

   fun print() {
      print(root)
   }

   private fun print(x: Node?) {
      if (x == null) return
      print(x.left)
      println(x.key)
      print(x.right)
   }

   fun keys(): Iterable<Key> = keys(min(), max())

   fun keys(low: Key, high: Key): Iterable<Key> {
      val queue = LinkedList<Key>()
      keys(root, queue, low, high)
      return queue
   }

   private fun keys(x: Node?, queue: Queue<Key>, low: Key, high: Key) {
      if (x == null) return
      val cmpLow = low.compareTo(x.key)
      val cmpHigh = high.compareTo(x.key)
      if (cmpLow < 0) keys(x.left, queue, low, high)
      if (cmpLow <= 0 && cmpHigh >= 0) queue.add(x.key)
      if (cmpHigh > 0) keys(x.right, queue, low, high)
   }
}
```
