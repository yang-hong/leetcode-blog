## 🧩 Problem
https://leetcode.com/problems/max-area-of-island/description/

## 💭 My thinking process
For each cell(grid[r][c]), if we find that cell is 1(island), we make the maxArea the max of currArea or dfs's returned area, and then use dfs to make neighbor's 1 to 0. End the dfs when it is out of boundaries and neighboring cell is 0. Under dfs, we have curr_area as 1 because we already found one area of island. And we do curr_area += dfs(neighbors) to add the areas to its neighbors and we return the curr_area at last

## 💡 Things I have challenges with
1. For nested for loops, don't call dfs and then call dfs again when calculating maxArea. First dfs will make every cell 0, so the answer will always be zero. Instead maxArea = max(maxArea, dfs(r, c))
2. Dfs, need to return curr_area at last because we need that value to pass to maxArea
3. 1 and 0 is int instaed of string

## 🧠 Code
```
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        rows = len(grid)
        cols = len(grid[0])
        res = 0

        def bfs(r, c):
            queue = deque()
            queue.append((r, c))
            grid[r][c] = '0'

            while queue:
                x, y = queue.popleft()
                for dx, dy in [(1,0), (-1,0), (0,1), (0,-1)]:
                    nx, ny = x + dx, y + dy

                    if 0 <= nx < rows and 0 <= ny < cols and grid[nx][ny] == '1':
                        grid[nx][ny] = '0'
                        queue.append((nx, ny))

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':
                    res += 1
                    bfs(r, c)

        return res
```

## 📈 Complexity
O(m*n)
O(m*n)