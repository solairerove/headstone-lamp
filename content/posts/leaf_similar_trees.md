---
title: 872. Leaf-Similar Trees
description: dfs
date: 2024-01-09
tags: [ trees, dfs-bfs, easy ] 
---

```python
# O(n) time || O(h) space
# n - number of all nodes
# h - height of tree
def leaf_similar(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
    def dfs(node: TreeNode):
        if not node:
            return []

        if not node.left and not node.right:
            return [node.val]

        return dfs(node.left) + dfs(node.right)

    return dfs(root1) == dfs(root2)
```

The approach to solving this problem involves two main steps:

1) Traverse each tree to collect its leaf values: We can do this using either depth-first search (DFS) or breadth-first
   search (BFS). DFS is more straightforward in this case as it allows us to easily access the leaves.

2) Compare the leaf value sequences: Once we have the leaf sequences from both trees, we compare them to determine if
   they are identical.

Here's a general outline of the algorithm:

1) Define a function `dfs` that performs DFS on a given tree and collects its leaf values in a list.
2) Apply `dfs` to both `root1` and `root2`.
3) Compare the two sequences. If they are identical, return `true`. Otherwise, return `false`.