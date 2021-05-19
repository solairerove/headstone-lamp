---
title: "Caesar Cipher Encryptor"
date: 2021-05-17T19:58:00+03:00
draft: true
categories: ["strings"]
---

Input: "abc" \
Output: "cde"

[caesar cipher encryptor](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/CaesarCipherEncryptor.kt)

```kotlin
// O(n) time | O(n) space
fun caesarCipherEncryptor(s: String, k: Int): String {
    val newLetters = mutableListOf<Char>()
    val key = k % 26
    s.forEach { newLetters.add(getNewLetter(it, key)) }

    return newLetters.joinToString("")
}

fun getNewLetter(letter: Char, key: Int): Char {
    val newLetterCode = letter.toInt() + key
    return if (newLetterCode <= 122) {
        newLetterCode.toChar()
    } else (newLetterCode % 122).toChar()
}
```
