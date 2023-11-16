---
title: 113. Path Sum II
description: dfs,
date: 2023-11-16
tags: [ trees, dfs-bfs, medium ] 
---

```python
# O(n) time || O(max(n, log(n)) space
def path_sum_rec(self, root: Optional[TreeNode], target_sum: int) -> List[List[int]]:
    if not root:
        return []

    res = []

    def dfs(node, curr_sum, curr_path):
        if not node:
            return

        curr_sum += node.val
        curr_path.append(node.val)

        if not node.left and not node.right and curr_sum == target_sum:
            res.append(list(curr_path))

        dfs(node.left, curr_sum, curr_path)
        dfs(node.right, curr_sum, curr_path)

        curr_path.pop()

    dfs(root, 0, [])

    return res
```

```python
# O(n) time || O(max(n, log(n)) space
def path_sum_dfs(self, root: Optional[TreeNode], target_sum: int) -> List[List[int]]:
    if not root:
        return []

    res = []
    stack = [(root, root.val, [root.val])]
    while stack:
        node, curr_sum, curr_path = stack.pop()

        if not node.left and not node.right and curr_sum == target_sum:
            res.append(curr_path)

        if node.left:
            stack.append((node.left, curr_sum + node.left.val, curr_path + [node.left.val]))

        if node.right:
            stack.append((node.right, curr_sum + node.right.val, curr_path + [node.right.val]))

    return res
```

To solve this problem, we can use a Depth-First Search (DFS) approach. We'll traverse the tree from the root to each
leaf, maintaining the current path and the sum of node values along the path. Whenever we reach a leaf node, we'll check
if the sum equals `targetSum`, and if it does, we'll add the current path to our list of valid paths.

1) Recursive DFS Function:
    - The `dfs` function takes a `node`, the `current_sum` of the path from the root to this node, and the
      current `path` (a list of node values).
    - If the node is `None`, we return as there's nothing to process.
    - The node's value is added to both the `current_sum` and the `path`.
    - If the node is a leaf (no left or right child) and `current_sum` equals `targetSum`, we add a copy of the current
      path to the result list.

2) Exploring Left and Right Subtrees:
    - Recursively call `dfs` for the left and right children of the current node, passing along the updated sum and
      path.

3) Backtracking:
    - After exploring a node (including its subtrees), we pop its value from the path to backtrack. This step is crucial
      as it ensures that the path list correctly represents the path from the root to the current node in the DFS.

4) Storing and Returning Results:
    - The `result` list accumulates all the valid paths. This list is returned at the end.

This approach ensures that all root-to-leaf paths are explored and the correct paths that sum to `targetSum` are
recorded. The use of backtracking is key to manage the current path state as we traverse the tree.
