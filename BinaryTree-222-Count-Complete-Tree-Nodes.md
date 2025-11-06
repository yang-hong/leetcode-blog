## 🧩 Problem
https://leetcode.com/problems/count-complete-tree-nodes/

## 💭 My thinking process
If there is both left and right, traverse left.left, and right.right, and write down the height. After traversal ends, there are two situations. If there is no left and right under current node, meaning it is a full tree, so we can use the formula: height ** 2 - 1. If there is either left or right, meaning it is a complete tree, so we have to traverse left and right and add their count + 1 (current node)

## 💡 Things I have challenges with
1. We need to assume for this question, it has to be a complete tree. With that condition, we can safely to only check left.left, right.right to know if it is a full tree
2. A binary tree is full if every node has either 0 or 2 children — no node has only one child
3. A binary tree is complete if: All levels except possibly the last are completely filled, and All nodes in the last level are as far left as possible

## 🧠 Code
```
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        left, right = root.left, root.right
        count = 1
        while left and right:
            count += 1
            left = left.left; right = right.right
        if not right and not left:
            #means it is full tree. use the formula to calculate the tree directly and return
            return 2 ** count - 1
        else:
            #means it is complete tree, we need to calculate the left and right node normally use recursion
            return 1 + self.countNodes(root.left) + self.countNodes(root.right)
```

## 📈 Complexity
🟢 最优情况（每次遇到满二叉树）

如果树是完美的或接近完美的：

每次都能通过 2 ** h - 1 公式直接返回，不再递归。

只需算一次高度 → O(log n)

🔵 平均情况 / 次优情况

大部分节点不是满的，但递归深度有限：

左右高度计算：O(h)

总共递归大约 log n 层（因为树是完全的）

→ O((log n)²)

🔴 最坏情况（极端不平衡）

虽然完全二叉树不会太不平衡，但理论上：

高度约 log n

每层都递归两边 → O(n)
（这种情况在“完全二叉树”中几乎不会发生）

| 类型       | 时间复杂度           | 空间复杂度        | 说明        |
| -------- | --------------- | ------------ | --------- |
| 最优（满二叉树） | **O(log n)**    | **O(log n)** | 高度计算一次    |
| 平均 / 常见  | **O((log n)²)** | **O(log n)** | 每层递归都计算高度 |
| 最坏       | **O(n)**        | **O(log n)** | 理论极端情况    |

logn 也可以用h代替