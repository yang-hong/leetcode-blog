## 🧩 Problem
https://leetcode.com/problems/binary-tree-preorder-traversal/

## 💭 My thinking process
Have a result array to store the resulting node. Loop through each node and add the node to result immediately, and continue loop through the node.left and node.right until you see the node is None, return to the upper level

## 💡 Things I have challenges with
1. Need to call dfs() under the main function
2. Don't need to return anything
3. Three criteria for dfs (1. input value and return type 2. end condition 3. operation for each level)
4. Append node.val instead of node itself

## 🧠 Code
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        
        def dfs(node): 
            if node is None:
                return
            
            res.append(node.val)
            dfs(node.left)
            dfs(node.right)
        
        dfs(root)
        return res
```

## 📈 Complexity
| Metric              | Complexity | Explanation                   |
| ------------------- | ---------- | ----------------------------- |
| **Time**            | O(n)       | Visit each node once          |
| **Auxiliary Space** | O(h)       | Recursion depth = tree height |
| **Total Space**     | O(n)       | Including output list         |
