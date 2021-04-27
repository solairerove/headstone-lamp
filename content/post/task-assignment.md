---
title: "Task Assignment"
date: 2021-04-27T22:23:32+03:00
draft: true
categories: ["greedy"]
---

Найти максимальную сумму скоростей тандема велосипедистов.

Input: tasks = [2, 4, 6, 1, 5, 3], k = 3 \
Output: [[3, 2], [0, 4], [5, 1]]

[task assignment](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/TaskAssignment.kt)

```kotlin
// O(nlog(n)) time | O(n) space
fun taskAssignment(tasks: MutableList<Int>, k: Int): List<List<Int>> {
    val paired = mutableListOf<List<Int>>()
    val taskDurationToIndices = taskDurationToIndices(tasks)

    tasks.sort()
    for (i in 0 until k) {
        val loTaskDuration = tasks[i]
        val loTaskIndices = taskDurationToIndices[loTaskDuration]!!
        val loIdx = loTaskIndices.removeAt(loTaskIndices.size - 1)

        val hiTaskDuration = tasks[tasks.size - 1 - i]
        val hiTaskIndices = taskDurationToIndices[hiTaskDuration]!!
        val hiIdx = hiTaskIndices.removeAt(hiTaskIndices.size - 1)

        paired.add(listOf(loIdx, hiIdx))
    }

    return paired
}

fun taskDurationToIndices(tasks: MutableList<Int>): MutableMap<Int, MutableList<Int>> {
    val taskDurationToIndices = mutableMapOf<Int, MutableList<Int>>()

    for (i in 0 until tasks.size) {
        val taskDuration = tasks[i]
        if (taskDuration in taskDurationToIndices) {
            taskDurationToIndices[taskDuration]!!.add(i)
        } else {
            taskDurationToIndices[taskDuration] = mutableListOf(i)
        }
    }

    return taskDurationToIndices
}
```
