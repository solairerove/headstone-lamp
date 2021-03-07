---
title: "Naive Huffman Encode"
date: 2021-03-07T15:55:23+03:00
draft: true
---

[Формулировка задачи](https://neerc.ifmo.ru/wiki/index.php?title=%D0%90%D0%BB%D0%B3%D0%BE%D1%80%D0%B8%D1%82%D0%BC_%D0%A5%D0%B0%D1%84%D1%84%D0%BC%D0%B0%D0%BD%D0%B0)

[naive huffman encode](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/greedy/NaiveHuffmanEncode.kt)

```kotlin
/**
 * abacabad
 * 4 14
 * a: 0
 * b: 10
 * c: 110
 * d: 111
 * 01001100100111
 */
fun main() {
    val s = "abacabad"

    val letterToFreq = getLetterToFrequency(s = s)
    val letterWeightStack = getLetterWeightStack(letterToFreq = letterToFreq)
    val huffmanResult = huffman(letterWeightStack = letterWeightStack)
    val dictionary = getDictionary(huffmanResult = huffmanResult)

    val encodedString = encodeString(stringToEncode = s, dictionary = dictionary)
    println("${dictionary.keys.size} ${encodedString.length}")
    dictionary.forEach { println("${it.key}: ${it.value}") }
    println(encodedString)
}

fun getLetterToFrequency(s: String): Map<String, Int> {
    val letterToFreq = HashMap<String, Int>()
    for (l in s) {
        val letter = l.toString()
        if (letterToFreq.containsKey(letter)) {
            letterToFreq[letter] = letterToFreq[letter]!!.plus(1)
        } else {
            letterToFreq[letter] = 1
        }
    }

    return letterToFreq
}

fun getLetterWeightStack(letterToFreq: Map<String, Int>): MutableList<LetterWeight> {
    return letterToFreq.map { LetterWeight(it.key, it.value) }.toMutableList()
}

fun getMinLetterWeight(letterWeightStack: MutableList<LetterWeight>): LetterWeight {
    var min = 0;
    for (i in letterWeightStack.indices) {
        if (letterWeightStack[i].weight < letterWeightStack[min].weight) {
            min = i
        }
    }
    return letterWeightStack.removeAt(min)
}

fun huffman(letterWeightStack: MutableList<LetterWeight>): List<List<String>> {
    val huffmanResult = mutableListOf<List<String>>()
    if (letterWeightStack.size == 1) {
        val letterWeight = getMinLetterWeight(letterWeightStack)
        huffmanResult.add(listOf(letterWeight.letter, "0"))
        return huffmanResult
    }
    while (letterWeightStack.size > 1) {
        val leftLetterWeight = getMinLetterWeight(letterWeightStack)
        val rightLetterWeight = getMinLetterWeight(letterWeightStack)

        val newLetter = leftLetterWeight.letter.plus(rightLetterWeight.letter)
        val newWeight = leftLetterWeight.weight.plus(rightLetterWeight.weight)

        val newLetterWeight = LetterWeight(letter = newLetter, weight = newWeight)
        letterWeightStack.add(newLetterWeight)

        huffmanResult.add(listOf(leftLetterWeight.letter, "0"))
        huffmanResult.add(listOf(rightLetterWeight.letter, "1"))
    }

    return huffmanResult
}

fun getDictionary(huffmanResult: List<List<String>>): Map<String, String> {
    val dictionary = mutableMapOf<String, String>()

    for (innerList in huffmanResult) {
        val letters = innerList[0]
        val code = innerList[1]

        letters.forEach { dictionary.merge(it.toString(), code) { a, b -> b.plus(a) } }
    }

    return dictionary
}

fun encodeString(stringToEncode: String, dictionary: Map<String, String>): String {
    val stringBuilder = StringBuilder()
    stringToEncode.forEach { stringBuilder.append(dictionary[it.toString()]) }

    return stringBuilder.toString()
}

data class LetterWeight(
    val letter: String,
    val weight: Int
)
```
