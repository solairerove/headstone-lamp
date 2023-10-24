---
title: 49. Group Anagrams
description: for each string in the given array, sort its characters and use the sorted string as a key to the hashmap
date: 2023-10-24
tags: [ array, medium ] 
---

```python
# O(w * n * log(n)) time || O(wn) space
def group_anagrams(self, strs: List[str]) -> List[List[str]]:
    dic = collections.defaultdict(list)

    for s in strs:
        dic[tuple(sorted(s))].append(s)

    return list(dic.values())
```

```python
# O(n * m) time || O(n * m) space,
# m - number of strings
# n - average number of letters
def group_anagrams_count_approach(self, strs: List[str]) -> List[List[str]]:
    def get_key(s):
        cnt = [0] * 26
        for c in s:
            cnt[ord(c) - ord('a')] += 1

        return tuple(cnt)

    dic = collections.defaultdict(list)
    for s in strs:
        dic[get_key(s)].append(s)

    return list(dic.values())
```

For each string in the given array, sort its characters and use the sorted string as a key to the hashmap. \
Append the original string to the list associated with the key in the hashmap.

Small improvement

    For each string, count the frequency of each character.
    Convert these counts into a tuple of 26 elements (for each of the lowercase English letters).
    Use this tuple as a key to the hashmap.

Return the values of the hashmap.