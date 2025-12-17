## 🧩 Problem
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

## 💭 My thinking process
We traverse the whole tree, and from leaf to root. We need to pass the value from each level of node. The value we pass include: if left side of tree is not None and right side of tree is not None, we return curr node value. If either side of the tree is None, we return the other side's value

## 💡 Things I have challenges with
1. If we need to search from bottom to root, it is postorder traversal, and we need to return the value from bottom level to top level, so we need to have a variable to call the traversal function. like left = dfs(root.left). If we only need to traverse from top to down, then we can just directly call dfs(root.left)

## 🧠 Code
```
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root:
            return None
        
        if root.val == p.val:
            return p
        
        if root.val == q.val:
            return q
        
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)

        if left is not None and right is not None:
            return root
        
        if left is not None and right is None:
            return left
        
        if left is None and right is not None:
            return right
        
        return None

```

## 📈 Complexity
| Case          | Time Complexity | Space Complexity |
| ------------- | --------------- | ---------------- |
| Balanced Tree | O(N)            | O(log N)         |
| Skewed Tree   | O(N)            | O(N)             |

