## 🧩 Problem
https://leetcode.com/problems/symmetric-tree/

## 💭 My thinking process
Recursively compare left node and right node. If they have equal value, we need to further compare its children. For iterative approach, we create a queue(or stack) and put [node.left, node.right]. We pop this and compare, if it is equal, we further put [node.left.left, node.right.right], [node.left.right, node.right.left]

## 💡 Things I have challenges with
1. We are not comparing the node. We are comparing the the whole tree under that node. So under the compare recursion, we call the recursion again to further compare

## 🧠 Code
```
# Recursion
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return
        
        def compare(left, right):
            if not left and not right:
                return True
            elif not left or not right:
                return False
            elif left.val != right.val:
                return False
            return left.val == right.val and compare(left.left, right.right) and compare(left.right, right.left)
        
        return compare(root.left, root.right)
```

```
from collections import deque

class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True
        q = deque([(root.left, root.right)])

        while q:
            left, right = q.popleft()
            if not left and not right:
                continue
            if not left or not right or left.val != right.val:
                return False
            q.append((left.left, right.right))
            q.append((left.right, right.left))
        return True

```