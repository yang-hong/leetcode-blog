## 🧩 Problem
https://leetcode.com/problems/path-sum-ii/

## 💭 My thinking process
Have result and path array. Run dfs with no return value. We will need to calculate the remainingSum under each recursion. If remainingSum is 0, meaning we have a valid path. We need to hardcopy the path to result. After each level of recursion. we need to do the backtrack(path.pop()) because we are not returning(saving) path to each level of recursion

## 💡 Things I have challenges with
| Question                                   | Answer                                                                                  |
| ------------------------------------------ | --------------------------------------------------------------------------------------- |
| Why not `return dfs(left) and dfs(right)`? | Because we need to explore both fully, not stop early.                                  |
| Why pass `remaining`?                      | To carry the current remaining target down each recursion.                              |
| Why not return `remaining`?                | We’re building results in a list, not computing a single value.                         |
| Why `path.pop()`?                          | To undo the last choice and restore the previous path before exploring the next branch. |
| Why not rely on `return` for backtracking? | Because `return` doesn’t change `path` — all calls share the same list reference.       |
| Why `path.copy()`?                         | To store a snapshot of the path before it changes later.                                |


## 🧠 Code
```
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        result = []
        path = []

        def dfs(node, remaining):
            if not node:
                return

            path.append(node.val)
            remaining -= node.val

            if not node.left and not node.right and remaining == 0:
                result.append(path.copy())  # snapshot of current path

            dfs(node.left, remaining)
            dfs(node.right, remaining)

            path.pop()  # backtrack to previous state

        dfs(root, targetSum)
        return result

```

## 📈 Complexity
| Measure           | Complexity                 | Notes                                       |
| ----------------- | -------------------------- | ------------------------------------------- |
| **Time**          | O(n + L × h) → worst O(n²) | Traverse all nodes and copy each valid path |
| **Space (stack)** | O(h)                       | Depth of recursion                          |
| **Output size**   | O(L × h)                   | Total number of stored paths                |
