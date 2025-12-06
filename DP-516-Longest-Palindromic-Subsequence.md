## 🧩 Problem
https://leetcode.com/problems/longest-palindromic-subsequence/description/

## 💭 My thinking process
dp[i][i], which is for all the diagnoal cell, initialized as 1 because character itself has length of 1 palindrome. From bottom left, if s[i] == s[j], meaning these 2 characters are same, if we can determine the numbers inside these 2 numbers is the palindrome, we use that cell dp[i + 1][j - 1] + 2. If they are not the same, we either delete the character on the right (i) or character on the left(j) and choose the maximum number (dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]))

## 💡 Things I have challenges with

## 🧠 Code
```
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        dp = [[0] * len(s) for i in range(len(s))]

        for i in range(len(s)):
            dp[i][i] = 1
        
        for i in range(len(s) - 1, -1, -1):
            for j in range(i + 1, len(s)):
                if s[i] == s[j]:
                    dp[i][j] = dp[i + 1][j - 1] + 2
                else:
                    dp[i][j] = max(dp[i + 1][j], dp[i][j - 1])
        
        return dp[0][-1]
```

## 📈 Complexity
Time: O(n*n)
Space: O(n*n)