---
title: "Huffman Decode"
date: 2021-03-07T18:25:44+03:00
draft: true
categories: ["greedy"]
---

[Формулировка задачи](https://neerc.ifmo.ru/wiki/index.php?title=%D0%90%D0%BB%D0%B3%D0%BE%D1%80%D0%B8%D1%82%D0%BC_%D0%A5%D0%B0%D1%84%D1%84%D0%BC%D0%B0%D0%BD%D0%B0)

[huffman decode](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/HuffmanDecode.kt)

```kotlin
// abacabad
fun main() {
    val dictionary = mapOf(
        Pair("0", "a"),
        Pair("10", "b"),
        Pair("110", "c"),
        Pair("111", "d")
    )

    val s = "01001100100111"

    val stringBuilder = StringBuilder()
    var i = 0
    while (i < s.length) {
        var isCodeFound = false
        var code = s[i].toString()
        while (!isCodeFound) {
            if (dictionary.containsKey(code)) {
                stringBuilder.append(dictionary[code])
                isCodeFound = true
            } else {
                code = code.plus(s[++i].toString())
                isCodeFound = false
            }
        }
        i++
    }

    print(stringBuilder.toString())
}
```
