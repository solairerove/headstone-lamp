---
title: "Dutch National Flag"
date: 2021-04-14T23:04:03+03:00
draft: true
categories: ["sorting"]
---

Дан массив для сортировки, и массив числе в порядке, в котором нужно отсортировать.

Есть несколько решений.
- пройтись и посчитать сколько встречается элемент и потом перезаписать
- выставить за проход первый элемент, за второй выставить третий элемент
- дейкстра стайл

[dutch national flag](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/sorting/DutchNationalFlag.kt)

```kotlin
// O(n) time | O(1) space
fun sortColors(arr: MutableList<Int>, colors: List<Int>) {
    var lt = 0
    var i = 0
    var gt = arr.size - 1

    while (i <= gt) {
        when (arr[i]) {
            colors[0] -> swap(arr, i++, lt++)
            colors[1] -> i++
            else -> swap(arr, i, gt--)
        }
    }
}

fun swap(arr: MutableList<Int>, i: Int, j: Int) {
    val temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}
```
