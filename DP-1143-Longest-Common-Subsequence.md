## 🧩 Problem
https://leetcode.com/problems/longest-common-subsequence/

## 💭 My thinking process
2D array. dp[i][j] = LCS length of text1[:i] and text2[:j]. If not equal, drop either curr i or j and take the max of them. If equal, take the previous lengh + 1

## 💡 Things I have challenges with
1. dp table is len(text1) + 1 len(text2) + 1
2. For loop starts from 1 and ends at len + 1. 1 to len + 1 will covers all the chars of string
3. return dp[m][n] instead of m + 1, n + 1 because dp table starts with index 0 instead of 1! so the last index should be m instead of m + 1

## 🧠 Code
```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        # dp[i][j] = LCS length of text1[:i] and text2[:j]
        dp = [[0] * (n + 1) for _ in range (m + 1)]

        for i in range (1, m + 1):
            for j in range(1, n + 1):
                if text1[i - 1] == text2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                else:
                    dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])
        
        return dp[m][n]
```

## 📈 Complexity
Time: O(n)
Space: O(n * n)