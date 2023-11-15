---
title: 110. Balanced Binary Tree
description: you can solve it the same method as in leetcode 100 same tree
date: 2023-11-15
tags: [ trees, easy ] 
---

```python
# O(n) time || O(n) space
def is_balanced(self, root: Optional[TreeNode]) -> bool:
    def dfs(node):
        if not node:
            return 0, True

        l_height, l_balanced = dfs(node.left)
        r_height, r_balanced = dfs(node.right)

        return max(l_height, r_height) + 1, l_balanced and r_balanced and abs(l_height - r_height) <= 1

    return dfs(root)[1]
```

DFS is ideal for this problem because it allows us to compute the height of each subtree while simultaneously checking
if the tree is balanced.

In DFS, we recursively traverse down the tree, visiting a node's children before checking the node itself (hence "
depth-first"). This method is particularly efficient for tree problems like this one, where we need to gather
information from the bottom (leaf nodes) up to the top (root node).

Here's how the DFS works in the context of checking if a tree is height-balanced:

1) Recursive Traversal: The check function is called recursively on each node's left and right children. This traversal
   goes down to the leaf nodes of the tree.

2) Height Calculation: At each node, after the recursive calls return, we calculate the height of the subtree rooted at
   that node. The height is determined based on the heights of the left and right subtrees, which are obtained from the
   recursive calls.

3) Balance Check: Along with the height calculation, we also check whether the current subtree is balanced. This is done
   by checking the height difference between the left and right subtrees. If the difference is more than 1, the subtree
   is not balanced.

4) Propagating Information Upward: The function returns two pieces of information for each node: its subtree height and
   whether it is balanced. This information is then used by the parent node to perform its own balance check and height
   calculation.

5) Final Result: The process continues until the root node, where we get the final decision on whether the whole tree is
   balanced.

This approach ensures that each node and its subtrees are only visited once, making it a time-efficient solution. The
DFS strategy is effective here as it allows for the necessary computations and checks to be made at each step in a
single pass through the tree.