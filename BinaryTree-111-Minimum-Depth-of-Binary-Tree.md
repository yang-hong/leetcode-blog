## 🧩 Problem
https://leetcode.com/problems/minimum-depth-of-binary-tree/

## 💭 My thinking process
To define a min depth, it is the min depth from root to leave node. Leave node is defined as when there is no children. If we find a node that has left or right, we run the recursion on left or right, else we run recursion on both side

## 💡 Things I have challenges with
1. Leave node is defined as when there is no children

## 🧠 Code
```
# Recursion
class Solution:
    def minDepth(self, root):
        if root is None:
            return 0
        if root.left is None and root.right is not None:
            return 1 + self.minDepth(root.right)
        if root.left is not None and root.right is None:
            return 1 + self.minDepth(root.left)
        return 1 + min(self.minDepth(root.left), self.minDepth(root.right))
```