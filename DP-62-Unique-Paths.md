## 🧩 Problem
https://leetcode.com/problems/unique-paths/description/

## 💭 My thinking process
To reach position i, how many ways? base case: cell(0,0) is 1 and all (0, c) and (r, 0) are 1. Transaction function: dp[i - 1][j] + dp[i][j - 1]

## 💡 Things I have challenges with
1. 2d array: dp = [[1] * n for _ in range(m)]
2. All (0, c), and (r, 0) are already filled with 1 in initialization, so don't need to refill
3. Starting from index 1 and end at row and col(not inclusive): for i in range(1, row)

## 🧠 Code
```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        #to reach position i, how many ways? base case is cell(0,0) is 1, and all (0,c) and (r, 0) are 1
        dp = [[1] * n for _ in range(m)]
        #start from cell(1,1)
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        
        return dp[m - 1][n - 1]
```

## 📈 Complexity
Time: O(m * n)
Space: O(m * n)