## 🧩 Problem
https://leetcode.com/problems/number-of-islands/description/

## 💭 My thinking process
For each cell(grid[r][c]), if we find that cell is 1(island), we make result += 1, and then we need to perform dfs on its neighbors to make all neighboring land 0(drawning) to make sure we won't recalculate the number of island. After we hit the boundaries and we see the water(0), we stop the dfs and return 我们要淹没整个岛屿

## 💡 Things I have challenges with
1. grid[r][c] = '0' Need to be = instead of ==
2. need to call recursion dfs(r + 1, c)
3. range(rows). there is column

## 🧠 Code
```
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        rows = len(grid)
        cols = len(grid[0])
        res = 0

        def dfs(r, c):
            if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] == '0':
                return
            
            grid[r][c] = '0'
            #make other directions 0
            dfs(r + 1, c)
            dfs(r - 1, c)
            dfs(r, c + 1)
            dfs(r, c - 1)

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':
                    res += 1
                    dfs(r, c)

        return res
```

## 📈 Complexity
O(m*n)
O(m*n)