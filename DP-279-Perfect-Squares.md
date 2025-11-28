## 🧩 Problem
https://leetcode.com/problems/perfect-squares/

## 💭 My thinking process
This is a complete backpack question because we can select multiple number of coins. To get the newest number of conis, our dp function as to return the min of curr dp[i], which is not selecting the current coin, and dp[i - coin] + 1, which is selecting the current coin. Also, we need to make sure i always >= coin

## 💡 Things I have challenges with
1. [float('inf')] * (n + 1). Ther should be braket 
2. for j in range(1, int(sqrt(i)) + 1) or int(i ** 0.5) because we only want to interate j*j <= i

## 🧠 Code
```
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [float('inf')] * (n + 1)
        dp[0] = 0
        
        for i in range(1, n + 1):
            for j in range(1, int(sqrt(i)) + 1):
                if i - j >= 0:
                    dp[i] = min(dp[i], dp[i - j * j] + 1)
        
        return dp[-1] if dp[i] != float('inf') else -1
```

## 📈 Complexity
Time: O(n √n)
Space: O(n)