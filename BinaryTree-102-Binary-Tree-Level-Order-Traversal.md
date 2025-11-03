## 🧩 Problem
https://leetcode.com/problems/binary-tree-level-order-traversal/

## 💭 My thinking process
Create a deque (FIFO) with root in deque. While deque has element, calculate the queue size first as level size (this is to track which level we are in). For each level size, pop the current queue node and put it to level array, and put its left and right to teh queue

## 💡 Things I have challenges with
1. queue = deque([root]) but not queue = deque(root)
| Expression       | What happens                           | Result               |
| ---------------- | -------------------------------------- | -------------------- |
| `deque([1,2,3])` | iterates through list [1,2,3]          | deque([1,2,3])       |
| `deque("abc")`   | iterates through string "abc"          | deque(['a','b','c']) |
| `deque(5)`       | ❌ int not iterable                     | TypeError            |
| `deque(root)`    | ❌ TreeNode not iterable                | TypeError            |
| `deque([root])`  | iterates through list with one element | deque([root]) ✅      |
2. level.append(node.val) not node itself!!!

## 🧠 Code
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        
        res = []
        queue = deque([root])

        while queue:
            level = []
            level_size = len(queue)

            for _ in range(len(queue)):
                node = queue.popleft()
                level.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            res.append(level)
        
        return res
```