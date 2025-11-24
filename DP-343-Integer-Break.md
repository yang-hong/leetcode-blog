## 🧩 Problem
https://leetcode.com/problems/unique-paths-ii/description/

## 💭 My thinking process
for each i, for each j (the number we substract from i), we do j * (i - j), or j * dp[i - j], which is to further divide j, and choose the maximum. dp[i] represent the maximum product for the interger i. dp[i] = max(dp[i], dp[i - j] * j, j * (i - j))

## 💡 Things I have challenges with
1. Need two for loops. Second for loop is to iteraterate which numbers to substract. But the dp table is still 1d table
2. dp[i] = max(dp[i], dp[i - j] * j, j * (i - j)). Need to have dp[i], because it will store the previous state, like when j = 1, we have a new dp[i], and when j = 2, we have a new dp[i]. If we don't store this, it will only have the value when j is the last value, which for sure is not the maximum product
3. j * (i - j) is divide to 2 numbers. dp[i - j] * j is further divide
4. j can iterate half of the index: i // 2 + 1 because production of cloest numbers are always the largest

## 🧠 Code
```
class Solution:
    def integerBreak(self, n: int) -> int:
        dp = [0] * (n + 1)
        dp[2] = 1 #base case

        for i in range(3, n + 1):
            for j in range(1, i // 2 + 1):
                dp[i] = max(dp[i], dp[i - j] * j, j * (i - j))
        
        print(dp)
        return dp[n]
```

## 📈 Complexity
Time: O(m * n)
Space: O(n)