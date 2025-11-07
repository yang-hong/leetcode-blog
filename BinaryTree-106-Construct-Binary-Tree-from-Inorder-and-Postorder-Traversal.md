## 🧩 Problem
https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/

## 💭 My thinking process
We use the last element from postorder as root ad separate the root index from inorder from left tree and right tree.

## 💡 Things I have challenges with
1. We need to process right tree first, and then left tree because for post order, it is [left, right, root]. So when we pop the next root, it is actually coming from right
2. self.buildTree(inorder[idx + 1:], postorder)


## 🧠 Code
```
class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        if not inorder or not postorder:
            return None
        
        root_val = postorder.pop()
        root = TreeNode(root_val)

        idx = inorder.index(root_val)
        
        root.right = self.buildTree(inorder[idx + 1:], postorder)
        root.left = self.buildTree(inorder[:idx], postorder)

        return root

```

## 📈 Complexity
Time Complexity = O(n)
Space Complexity = O(n) (hash map + recursion stack)