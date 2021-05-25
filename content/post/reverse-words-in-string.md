---
title: "Reverse Words in String"
date: 2021-05-25T18:43:36+03:00
draft: true
categories: ["strings"]
---

Input: "anything. do to free we're that everything lost we've after only It's" \
Output: "It's only after we've lost everything that we're free to do anything." \

[reverse words in string](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/ReverseWordsInString.kt)

```kotlin
// O(n) time | O(n) space
fun reverseWordsInString(s: String): String {
    val chars = s.map { it }.toMutableList()
    val n = chars.size
    reverse(chars, 0, n - 1)

    var low = 0
    while (low < n) {
        var high = low
        while (high < n && chars[high] != ' ') high++

        reverse(chars, low, high - 1)
        low = high + 1
    }

    return chars.joinToString("")
}

fun reverse(chars: MutableList<Char>, lo: Int, hi: Int) {
    var low = lo
    var high = hi

    while (low < high) {
        swap(chars, low, high)
        low++
        high--
    }
}

fun swap(arr: MutableList<Char>, i: Int, j: Int) {
    val tmp = arr[i]
    arr[i] = arr[j]
    arr[j] = tmp
}
```
