## 🧩 Problem
https://leetcode.com/problems/path-sum/

## 💭 My thinking process
Have a variable called targetSum. For each node visited, substract node from targetSum. If reach the leave of node (if not root.right and not root.left), we return if the targetSum is zero. We traverse node.left and node.right for all the path

## 💡 Things I have challenges with
1. This recursion has return value, so when not root, we need to return False instead of returning nothing

## 🧠 Code
```
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        
        targetSum -= root.val
        
        if not root.left and not root.right:
            if targetSum == 0:
                return True
        
        return self.hasPathSum(root.left, targetSum) or self.hasPathSum(root.right, targetSum)
```

## 📈 Complexity
| Complexity Type | Symbolic | Typical Value         |
| --------------- | -------- | --------------------- |
| **Time**        | O(n)     | visit every node once |
| **Space**       | O(h)     | recursion depth, ≤ n  |
