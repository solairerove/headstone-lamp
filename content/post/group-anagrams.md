---
title: "Group Anagrams"
date: 2021-05-11T21:08:31+03:00
draft: true
categories: ["strings"]
---

Input: ["funeral", "realfun", "debitcard", "badcredit", "bobmarley", "marbleboy"] \
Output: [[funeral, realfun], [debitcard, badcredit], [bobmarley, marbleboy]]

[group anagrams](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/strings/GroupAnagrams.kt)

```kotlin
// O(w * nlog(n)) time | O(wn) space
// w - number of words
// n - length of longest word
fun groupAnagrams(words: List<String>): List<List<String>> {
    val anagrams = mutableMapOf<String, MutableList<String>>()
    for (word in words) {
        val sortedWord = word.toCharArray().sortedArray().joinToString("")
        if (sortedWord in anagrams) {
            anagrams[sortedWord]!!.add(word)
        } else {
            anagrams[sortedWord] = mutableListOf(word)
        }
    }

    return anagrams.values.toList()
}
```
