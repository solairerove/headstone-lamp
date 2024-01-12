---
title: 235. Lowest Common Ancestor of a Binary Search Tree
description: dfs and use that we traverse bst
date: 2023-10-27
tags: [ trees, dfs-bfs, medium ]
---

```python
# O(h) time || O(h) space
def lowest_common_ancestor_dfs(self, root: TreeNode, p: TreeNode, q: TreeNode) -> Optional[TreeNode]:
    def dfs(node):
        if not node:
            return None

        if node.val < p.val and node.val < q.val:
            return dfs(node.right)

        if node.val > p.val and node.val > q.val:
            return dfs(node.left)

        return node

    return dfs(root)
```

1) Start from the root node.
2) Compare the values of the root with `p` and `q`:
    - If both `p` and `q` are greater than the root, then LCA lies in the right subtree. So, move to the right child of
      the root.
    - If both `p` and `q` are lesser than the root, then LCA lies in the left subtree. So, move to the left child of the
      root.
    - If one of `p` or `q` is less than the root and the other is greater, or if one of them is equal to the root, then
      the root is the LCA.
