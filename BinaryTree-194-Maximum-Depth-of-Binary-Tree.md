## 🧩 Problem
https://leetcode.com/problems/maximum-depth-of-binary-tree/

## 💭 My thinking process
Can use both recursion and iterative. If use recursion, calculate node.left depth and node.right depth, and compare and get the maximum and + 1 to get the current depth, and recurse up. If use iterative, have a depth variable 

## 💡 Things I have challenges with
1. know when to pass the self: self.maxDepth(root.left)

## 🧠 Code
```
# Recursion
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        leftDepth = self.maxDepth(root.left)
        rightDepth = self.maxDepth(root.right)
        maxDepth = max(leftDepth, rightDepth) + 1
        return maxDepth
```

```
from collections import deque

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        
        depth = 0
        queue = collections.deque([root])
        
        while queue:
            depth += 1
            for _ in range(len(queue)):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return depth
```