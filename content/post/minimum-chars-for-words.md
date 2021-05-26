---
title: "Minimum Chars for Words"
date: 2021-05-26T18:44:10+03:00
draft: true
categories: ["strings"]
---

Input: ["only", "after", "we", "have", "lost", "everything"] \
Output: [o, n, l, y, a, f, t, e, e, r, w, h, v, s, i, g] \

[minimum chars for words](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/MinimumCharsForWords.kt)

```kotlin
// O(n * l) time | O(c) space
// n is number of words
// l is length of longest word
// c is number of unique chars
fun minimumCharsForWords(words: List<String>): List<Char> {
    val maxCharFreq = mutableMapOf<Char, Int>()

    for (word in words) {
        val charFreq = mutableMapOf<Char, Int>()
        word.forEach { charFreq[it] = charFreq.getOrDefault(it, 0) + 1 }

        for ((char, freq) in charFreq) {
            if (char in maxCharFreq) {
                maxCharFreq[char] = max(freq, maxCharFreq[char]!!)
            } else {
                maxCharFreq[char] = freq
            }
        }
    }

    val chars = mutableListOf<Char>()
    for ((char, freq) in maxCharFreq) {
        for (i in 0 until freq) {
            chars.add(char)
        }
    }

    return chars
}
```
