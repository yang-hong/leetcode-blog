## 🧩 Problem
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

## 💭 My thinking process
We traverse from top to down. If the curr node value is less than p or q, meaning the common ancestor is on the right side of the node. If curr node value is larger than p or q, meaning the common ancestor is on the left side of the node. The reason being this is a BST, so when we find common ancestor, it has to be between [p,q]. Else we find the node, return the node

## 💡 Things I have challenges with
1. For iteration, we need to have a while loop (while root)
2. It has to include all the condition, if we miss one condition, when that one condition is excluded, the while loop will keep running but not jump into any of the if condition, so it will end up having infinite loop
3. q can be larger than p, so we need to also think of condition like if (p <= curr <= q)

## 🧠 Code
```
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        while root:
            if root.val > p.val and root.val > q.val:
                root = root.left
            elif root.val < p.val and root.val < q.val:
                root = root.right
            else:
                return root
        return None
```
```
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        if root.val > p.val and root.val > q.val:
            return self.lowestCommonAncestor(root.left, p, q)
        elif root.val < p.val and root.val < q.val:
            return self.lowestCommonAncestor(root.right, p, q)
        else:
            return root
```

## 📈 Complexity
| Case          | Time Complexity | Space Complexity |
| ------------- | --------------- | ---------------- |
| Balanced Tree | O(N)            | O(log N)         |
| Skewed Tree   | O(N)            | O(N)             |

