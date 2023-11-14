---
title: 101. Symmetric Tree
description: you can solve it the same method as in leetcode 100 same tree
date: 2023-11-14
tags: [ trees, easy ] 
---

```python
# O(n) time || O(n) space
def is_symmetric_rec(self, root: Optional[TreeNode]) -> bool:
    def is_mirror_tree(node1, node2):
        if not node1 and not node2:
            return True

        if not node1 or not node2 or node1.val != node2.val:
            return False

        return is_mirror_tree(node1.left, node2.right) and is_mirror_tree(node1.right, node2.left)

    return is_mirror_tree(root.left, root.right)
```

```python
# O(n) time || O(n) space
def is_symmetric_dfs(self, root: Optional[TreeNode]) -> bool:
    stack = [(root.left, root.right)]
    while stack:
        left, right = stack.pop()

        if not left and not right:
            continue

        if not left or not right or left.val != right.val:
            return False

        stack.append((left.left, right.right))
        stack.append((left.right, right.left))

    return True
```

```python
# O(n) time || O(n) space
def is_symmetric_bfs(self, root: Optional[TreeNode]) -> bool:
    dq = collections.deque([(root.left, root.right)])
    while dq:
        left, right = dq.popleft()

        if not left and not right:
            continue

        if not left or not right or left.val != right.val:
            return False

        dq.append((left.left, right.right))
        dq.append((left.right, right.left))

    return True
```
