## 🧩 Problem
https://leetcode.com/problems/unique-paths-ii/description/

## 💭 My thinking process
to reach position i, how many ways. If there is obstable, way becomes 0. Still add cells from left and top to get the ways. Also need to consider edge case when first row or firsrt col has obstacle

## 💡 Things I have challenges with
1. Need to use origional table for if condition for if it is obstable or not! not DP table
2. There is an edge case that if the first row and col has obstable, we need to have that cell return 0. If not, the first row and cell will always be initialized as 1. So we need a for loop to loop through the first row and col, and for each cell, it needs to return the previous cell value. If previous is 0, meaning there is no way to reach to this position, so we also return 0, else there is one way

## 🧠 Code
```
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        #to reach position i, how many ways. If there is obstable, way becomes 0. Still add cells from left and top to get the ways
        row = len(obstacleGrid)
        col = len(obstacleGrid[0])
        dp = [[1]* col for _ in range(row)]

        if obstacleGrid[0][0] == 1:
            return 0
        
        for c in range(1, col):
            if obstacleGrid[0][c] == 1:
                dp[0][c] = 0
            else:
                dp[0][c] = dp[0][c - 1]
        
        for r in range(1, row):
            if obstacleGrid[r][0] == 1:
                dp[r][0] = 0           
            else:
                dp[r][0] = dp[r - 1][0] 

        for r in range(1, row):
            for c in range(1, col):
                if obstacleGrid[r][c] == 1:
                    dp[r][c] = 0
                else:
                    dp[r][c] = dp[r - 1][c] + dp[r][c - 1]
        
        return dp[row - 1][col - 1]
```

## 📈 Complexity
Time: O(m * n)
Space: O(m * n)