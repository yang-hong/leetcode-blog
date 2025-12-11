## 🧩 Problem
https://leetcode.com/problems/number-of-islands/description/

## 💭 My thinking process
For each cell(grid[r][c]), if we find that cell is 1(island), we make result += 1, and then we need to perform bfs on its neighbors to make all neighboring land 0(drawning) to make sure we won't recalculate the number of island. We first add its own cell to queue, and then we popleft the queue, and explore its level1 neighbors. For all level1 neighbors, we only perform the operations if we don't hit the boundaries and we see the land(1), the operation is to change land(1) to 0, and add this cell to the queue(IMPOTANT!). If the neighbor is 0, we don't do anything. If all neighbors are 0, we don't add any cell to queue. Until the queue is exhausted, we return the bfs

## 💡 Things I have challenges with
1. explore neighbors: 
for dx, dy in [(1,0), (-1,0), (0,1), (0,-1)]:
                    nx, ny = x + dx, y + dy
2. grid[nx][ny] == '1'! nx and ny not x and y

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