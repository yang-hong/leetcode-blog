## 🧩 Problem
https://leetcode.com/problems/count-complete-tree-nodes/

## 💭 My thinking process
To find the bottom level, we can use queue to find (iterative approach). We have another variable called leftmost. First initialize leftmost as root.val. For each level, we use if i == 0 to find the leftmost node and update to the leftmost value

## 💡 Things I have challenges with
1. Queue size is written as len(queue)
2. use if i == 0 to know if it is the leftmost node

## 🧠 Code
```
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        queue = deque([root])
        leftmost = root.val

        while queue:
            size = len(queue)
            for i in range(size):
                node = queue.popleft()
                if i == 0:
                    leftmost = node.val
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return leftmost
```

## 📈 Complexity
| 项目    | BFS          | DFS           |
| ----- | ------------ | ------------- |
| 时间复杂度 | **O(n)**     | **O(n)**      |
| 空间复杂度 | **O(n)**（队列） | **O(h)**（递归栈） |

