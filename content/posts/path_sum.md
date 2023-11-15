---
title: 112. Path Sum
description: dfs, keeping track of the sum of node values. return true if the sum equals `targetSum` at any leaf
date: 2023-11-15
tags: [ trees, dfs-bfs, easy ] 
---

```python
# O(n) time || O(max(n, log(n)) space
def has_path_sum_rec(self, root: Optional[TreeNode], target_sum: int) -> bool:
    if not root:
        return False

    def dfs(node, curr_sum):
        if not node:
            return False

        curr_sum += node.val

        if not node.left and not node.right:
            return curr_sum == target_sum

        return dfs(node.left, curr_sum) or dfs(node.right, curr_sum)

    return dfs(root, 0)
```

```python
# O(n) time || O(max(n, log(n)) space
def has_path_sum_dfs(self, root: Optional[TreeNode], target_sum: int) -> bool:
    if not root:
        return False

    stack = [(root, root.val)]
    while stack:
        node, curr_sum = stack.pop()

        if not node.left and not node.right and curr_sum == target_sum:
            return True

        if node.left:
            stack.append((node.left, curr_sum + node.left.val))

        if node.right:
            stack.append((node.right, curr_sum + node.right.val))

    return False
```

Sure, this problem can be solved using a Depth-First Search (DFS) approach. The idea is to traverse the tree from the
root to each leaf, keeping track of the sum of node values along the path. If the sum equals `targetSum` at any leaf
node, we return `True`. If no such path is found by the time all nodes have been visited, we return `False`.

1) Base Case for Empty Tree: If the tree is empty (i.e., `root` is `None`), return `False`.

2) DFS Function:
    - This is a recursive function that takes a node and the current sum of values along the path from the root to this
      node.
    - If the node is `None`, return `False` (this happens when we reach a null child of a leaf node).
    - Add the node's value to `current_sum`.
    - If the current node is a leaf (both left and right children are `None`), check if `current_sum`
      equals `targetSum`. If yes, return `True`.
    - If the node is not a leaf, recursively call `dfs` on the left and right children, passing the updated sum. The
      function returns `True` if either subtree returns `True`.
3) Starting the DFS: The function begins DFS from the root node with an initial `current_sum` of 0.

This approach ensures that all root-to-leaf paths are checked, and the target sum condition is verified for each path.
The DFS efficiently explores each path one by one until it finds a match or exhausts all possibilities.
