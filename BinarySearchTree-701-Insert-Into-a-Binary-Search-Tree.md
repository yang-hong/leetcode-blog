
## 🧩 Problem
https://leetcode.com/problems/insert-into-a-binary-search-tree/description/

## 💭 My thinking process
Since this is a BST, it is already sorted. So we just need to find an empty node place and insert. To find where to insert, we need to check if node.left val is larger or smaller than inserted val. Return the curr node so that it will finallly return the root of the tree

## 💡 Things I have challenges with
1. Can't simply write root = root.left because we are not only traversing the tree, but also returning the head of the tree. root = root.left is more like a iterative approach, where we need to have a while root condition

## 🧠 Code
```
class Solution:
    def insertIntoBST(self, root, val):
        if root is None:
            node = TreeNode(val)
            return node

        if root.val > val:
            root.left = self.insertIntoBST(root.left, val)
        if root.val < val:
            root.right = self.insertIntoBST(root.right, val)

        return root
```

## 📈 Complexity
| Case         | Time Complexity | Space Complexity |
| ------------ | --------------- | ---------------- |
| Balanced BST | **O(log N)**    | **O(log N)**     |
| Skewed BST   | **O(N)**        | **O(N)**         |
