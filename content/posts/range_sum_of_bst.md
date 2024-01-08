---
title: 938. Range Sum of BST
description: dfs
date: 2024-01-08
tags: [ trees, dfs-bfs, easy ] 
---

```python
# O(n) time || O(h) space
# n - number of all nodes
# h - height of tree
def range_sum_bst(self, root: Optional[TreeNode], low: int, high: int) -> int:
    if not root:
        return 0

    if root.val < low:
        return range_sum_bst(self, root.right, low, high)
    elif root.val > high:
        return range_sum_bst(self, root.left, low, high)

    return root.val + range_sum_bst(self, root.left, low, high) + range_sum_bst(self, root.right, low, high)
```

```python
# O(n) time || O(h) space
def range_sum_bst_iterative(self, root: Optional[TreeNode], low: int, high: int) -> int:
    if not root:
        return 0

    stack, res = [root], 0
    while stack:
        node = stack.pop()
        if node:
            if node.val > low:
                stack.append(node.left)

            if node.val < high:
                stack.append(node.right)

            if low <= node.val <= high:
                res += node.val

    return res
```
