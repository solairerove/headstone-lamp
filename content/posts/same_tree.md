---
title: 100. Same Tree
description: traverse through trees and recognize if there's same structure and val
date: 2023-11-14
tags: [ trees, easy ] 
---

To solve this problem, we need to compare two binary trees, `p` and `q`, and determine if they are identical.
Two binary trees are identical if they have the same structure and their corresponding nodes have the same value.

```python
# O(n) time || O(h) space
def is_same_tree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
    if not p and not q:
        return True

    if not p or not q or p.val != q.val:
        return False

    return is_same_tree(self, p.left, q.left) and is_same_tree(self, p.right, q.right)
```

```python
# O(n) time || O(h) space
def is_same_tree_dfs(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
    stack = [(p, q)]
    while stack:
        node1, node2 = stack.pop()

        if not node1 and not node2:
            continue

        if not node1 or not node2 or node1.val != node2.val:
            return False

        stack.append((node1.left, node2.left))
        stack.append((node1.right, node2.right))

    return True
```

```python
# O(n) time || O(h) space
def is_same_tree_bfs(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
    dq = collections.deque([(p, q)])
    while dq:
        node1, node2 = dq.popleft()

        if not node1 and not node2:
            continue

        if not node1 or not node2 or node1.val != node2.val:
            return False

        dq.append((node1.left, node2.left))
        dq.append((node1.right, node2.right))

    return True
```
