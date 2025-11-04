## 🧩 Problem
https://leetcode.com/problems/invert-binary-tree/

## 💭 My thinking process
do preorder traversal and swap the node first, and then traverse left and then right. If we do inorder, the node will be swapped back, so we have to use node.left, and node.left twice to avoid that

## 💡 Things I have challenges with
1. Need to call dfs() under the main function
2. Don't need to return anything
3. Three criteria for dfs (1. input value and return type 2. end condition 3. operation for each level)
4. Append node.val instead of node itself

## 🧠 Code
```
# Definition for a binary tree node.
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        #base case
        if not root:
            return 
        
        root.left, root.right = root.right, root.left

        self.invertTree(root.left)
        self.invertTree(root.right)

        return root
```