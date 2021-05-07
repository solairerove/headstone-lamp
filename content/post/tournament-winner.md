---
title: "Tournament Winner"
date: 2021-05-07T15:18:41+03:00
draft: true
categories: ["arrays"]
---

Input:

```kotlin
val competitions = listOf(
    listOf("Kotlin", "Java"),
    listOf("Java", "Python"),
    listOf("Python", "Kotlin")
)

val results = listOf(1, 0, 0)
```

Output: Kotlin

[tournament winner](https://github.com/solairerove/algs4-leprosorium/blob/master/src/main/kotlin/com/github/solairerove/algs4/leprosorium/arrays/TournamentWinner.kt)

```kotlin
// O(n) time | O(k) space
// n - number of competitions
// k - number of teams
fun tournamentWinner(competitions: List<List<String>>, results: List<Int>): String {
    var winner = ""
    val teamToScore = mutableMapOf(winner to 0)

    for (i in competitions.indices) {
        val (home, away) = competitions[i]
        val score = results[i]

        val currWinner = if (1 == score) home else away

        if (currWinner !in teamToScore) {
            teamToScore[currWinner] = 0
        }

        teamToScore[currWinner] = teamToScore[currWinner]!! + 3

        if (teamToScore[currWinner]!! > teamToScore[winner]!!) {
            winner = currWinner
        }
    }

    return winner
}
```
