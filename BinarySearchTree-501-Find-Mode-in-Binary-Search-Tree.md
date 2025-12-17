## 🧩 Problem
https://leetcode.com/problems/find-mode-in-binary-search-tree/

## 💭 My thinking process
We use inorder to sort the BST. for BST left is always smaller than right. And then we have a prev pointer and compare with curr node. And we also have maxCount and curr Count and mode[] to keep track of the modes and counts. To find modes, we need to compare if the adjacent nodes are the same. To compare, we need to have a prev pointer initialized as Null. If prev == curr, then they are the same, we increase the count. If not, meaning they are not the same, we change count back to 1 and make prev node = curr node to start a new comparation. We also need to update the modes, if count > maxCount, meaning there is a new modes, so we update mode list and maxCount. For each it it is equal, meaning we found 2 modes, so we only append the node value

## 💡 Things I have challenges with
1. For internal function, so always need to call this function at the main function, or else the the result will be empty
2. Logic for comparing prev and curr pointer: prev = Null. If prev.val == node.val: count += 1, else: count == 1 (change back to its origional value), prev = node.val


## 🧠 Code
```
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        self.prev = None
        self.count = 0
        self.maxCount = 0
        self.modes = []

        def inorder(node):
            if not node:
                return
            
            inorder(node.left)
            
            #process the current node
            if self.prev == node.val:
                self.count += 1
            else:
                self.count = 1
                self.prev = node.val
            
            #process the modes list
            if self.count > self.maxCount:
                self.modes = [node.val]
                self.maxCount = self.count
            elif self.count == self.maxCount:
                self.modes.append(node.val)
            
            inorder(node.right)
        
        inorder(root)
        return self.modes

```

## 📈 Complexity
| Category           | Complexity          | Explanation              |
| ------------------ | ------------------- | ------------------------ |
| **Time**           | **O(n)**            | Each node processed once |
| **Space (stack)**  | **O(h)**            | Depth of recursion       |
| **Space (output)** | **O(k)**            | Number of modes          |
| **Total**          | **O(n)** worst case | If tree skewed and k ≈ n |
