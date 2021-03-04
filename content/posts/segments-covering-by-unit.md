---
title: "Segments Covering by Unit"
date: 2021-03-04T13:00:03+03:00
draft: true
---

Даны отрезки на прямой. Найти такие точки, которые лежат на всех заданных отрезках. 
Найденное множество должно быть минимальным по размеру.

Берем все концы отрезков (как левые, так и правые) и сортируем их. 
Для каждой точки сохраним номер отрезка. 
Также каким концом его она является (левым или правым). 
Учтем, что если есть несколько точек с одной координатой, то сначала будут идти левые концы, потом правые.

Заведём коллекцию, в которой будут храниться номера отрезков, рассматриваемых в данный момент. 
Идем по точкам в отсортированном порядке. 
Если текущая точка — левый конец, то добавляем номер её отрезка в коллекцию. 
Иначе если она является правым концом, то проверяем, не был ли покрыт этот отрезок (был ли он добавлен в коллекцию). 
Если он уже был покрыт (его нет в коллекции), то ничего не делаем и переходим к следующей точке. 
Иначе если же он ещё не был покрыт (находится в коллекции), то мы добавляем текущую точку в ответ, 
и замечаем, что все текущие отрезки (которые в коллекции) становятся покрытыми. Опустошаем коллекцию.

[segment covering by unit](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/SegmentCoveringByUnit.kt)

```kotlin
fun main() {
    val segments = listOf(
        listOf(4, 7),
        listOf(1, 3),
        listOf(2, 5),
        listOf(5, 6),
    )

    val points = mutableListOf<Point>()
    for (i in segments.indices) {
        val segment = segments[i]
        val leftPoint = Point(value = segment[0], segmentNum = i + 1, pointType = PointType.LEFT)
        val rightPoint = Point(value = segment[1], segmentNum = i + 1, pointType = PointType.RIGHT)
        points.add(leftPoint)
        points.add(rightPoint)
    }

    Collections.sort(points, Point.pointComparator)

    val segmentNums = mutableSetOf<Int>()
    val res = mutableListOf<Int>()
    for (currPoint in points) {
        val segmentNum = currPoint.segmentNum

        if (PointType.LEFT == currPoint.pointType) {
            segmentNums.add(segmentNum)
        } else {
            if (segmentNums.contains(segmentNum)) {
                segmentNums.clear()
                res.add(currPoint.value)
            }
        }
    }

    println(res.size)
    res.forEach { print("$it ") }
}

data class Point(
    val value: Int,
    val segmentNum: Int,
    val pointType: PointType
) {

    companion object {
        val pointComparator = Comparator<Point> { p1, p2 ->
            val valCompare = p1.value.compareTo(p2.value)

            if (valCompare == 0) {
                if (PointType.LEFT == p1.pointType) -1 else 1
            } else {
                valCompare
            }
        }
    }
}

enum class PointType {
    LEFT, RIGHT
}
```
