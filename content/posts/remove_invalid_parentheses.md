---
title: 301. Remove Invalid Parentheses
description:
date: 2023-10-26
tags: [ arrays, dfs-bfs, hard ]
---

```python
# O(n * 2 ^ n) time || O(2 ^ n) space
def remove_invalid_parentheses(self, s: str) -> List[str]:
    def is_valid(string):
        cnt = 0
        for c in string:
            if c == '(':
                cnt += 1
            elif c == ')':
                cnt -= 1

            if cnt < 0:
                return False

        return cnt == 0

    res = []
    dq, visited, found = collections.deque([s]), {str}, False
    while dq:
        curr_str = dq.popleft()
        if curr_str not in visited:
            visited.add(curr_str)

            if is_valid(curr_str):
                found = True
                res.append(curr_str)

            if not found:
                for i, c in enumerate(curr_str):
                    if c in "()":
                        dq.append(curr_str[:i] + curr_str[i + 1:])

    return res
```

The main idea is to use Breadth-First Search (BFS) to explore all possible strings formed by removing 0 or more
parentheses. We start with the original string and, at each BFS level, we generate all possible strings by removing a
single parenthesis. The key insight is that the first valid strings we encounter during our BFS traversal are the ones
formed by removing the minimum number of invalid parentheses.

### Detailed Steps:

1) Initialization:
   Use a queue for BFS. Initially, the queue contains only the original string.
   Use a set (seen) to keep track of strings that have been visited to avoid re-processing.
   Initialize a found flag to False. This flag helps us stop BFS as soon as we find valid strings.
2) BFS:
    - While the queue is not empty:
        - For each string in the current BFS level:
            - Check if it's valid.
            - If it's valid, mark found as True and add it to the result list.
            - If no valid string is found at the current level, generate all possible strings by removing a single
              parenthesis. Add
              these to the queue if they haven't been seen before.
3) Validity Check:
   To determine if a string is valid, we use a counter. Increment the counter for every open parenthesis and decrement
   for every close parenthesis. The string is valid if the counter never goes negative and ends up being zero.

### More details

```python
newStr = currentStr[:j] + currentStr[j + 1:]
```

We're creating a new string (newStr) by removing the character at index j from the current string (currentStr).

Let's break it down:

1) `currentStr[:j]`: This slices the string from the beginning up to, but not including, index j. It takes all characters
before the j-th character.
2) `currentStr[j+1:]`: This slices the string from the position after j till the end. So, it takes all characters after the
j-th character.
By concatenating these two slices together, we essentially remove the character at index j.

#### Example:
Suppose currentStr = "abcde" and j = 2.

1) `currentStr[:j]` would be "ab"
2) `currentStr[j+1:]` would be "de"
When you concatenate them: "ab" + "de" = "abde".

As you can see, the character at index 2 (which is "c") has been removed from the original string.