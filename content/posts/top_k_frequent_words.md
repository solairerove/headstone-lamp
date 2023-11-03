---
title: 692. Top K Frequent Words
description: heapq library to obtain the kth largest number in O(n * log(k * m)) time.
date: 2023-11-03
tags: [ arrays, heap, sorting, medium ]
---

sorting to obtain the top k frequent words in O(n + m * log(m)) time.

```python
# O(n + m * log(m)) time || O(m) space
# n is number of words in list
# m is number of unique words
# k is number of top freq words
def top_k_frequent_sorting(self, words: List[str], k: int) -> List[str]:
    cnt = collections.Counter(words)

    return sorted(cnt, key=lambda word: (-cnt[word], word))[:k]
```

heapq library to obtain the top k frequent words in O(n + k * log(m)) time.

```python
# O(n + k * log(m)) time || O(m) space
# n is number of words in list
# m is number of unique words
# k is number of top freq words
def top_k_frequent_heap(self, words: List[str], k: int) -> List[str]:
    heap = [(-freq, word) for word, freq in collections.Counter(words).items()]
    heapq.heapify(heap)

    return [heapq.heappop(heap)[1] for _ in range(k)]
```

heapq library to obtain the top k frequent words in # O(n * log(k)) time.

```python
class Pair:
    def __init__(self, word, freq):
        self.word = word
        self.freq = freq

    def __lt__(self, pair):
        return self.freq < pair.freq or (self.freq == pair.freq and self.word > pair.word)


# O(n * log(k)) time || O(n) space
# n is number of words in list
# k is number of top freq words
def top_k_frequent_min_heap(self, words: List[str], k: int) -> List[str]:
    cnt = collections.Counter(words)
    heap = []
    for word, freq in cnt.items():
        heapq.heappush(heap, Pair(word, freq))
        if len(heap) > k:
            heapq.heappop(heap)

    return [pair.word for pair in sorted(heap, reverse=True)]
```
