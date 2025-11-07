## 🧩 Problem
https://leetcode.com/problems/minimum-absolute-difference-in-bst/description/

## 💭 My thinking process
We use inorder to sort the BST. for BST left is always smaller than right. And then we have a prev pointer and compare with curr node 

## 💡 Things I have challenges with
1. For BST, if we use inorder, it is sorted
2. If not use helper function, when we reach the leaf node (if not root: return), the recursion will end immediately 


## 🧠 Code
```
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        self.minDiff = float('inf')
        self.prev = None

        def inorder(node):
            if not node:
                return 
            inorder(node.left)
            if self.prev is not None:
                self.minDiff = min(self.minDiff, node.val - self.prev)
            self.prev = node.val
            inorder(node.right)
        
        inorder(root)
        return self.minDiff

```

## 📈 Complexity
Time Complexity = O(n)
Space Complexity = Total space: O(h) → O(log n) for balanced BST, O(n) for skewed.