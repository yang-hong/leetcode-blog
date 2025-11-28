## 🧩 Problem
https://leetcode.com/problems/coin-change/description/

## 💭 My thinking process
This is a complete backpack question because we can select multiple number of coins. To get the newest number of conis, our dp function as to return the min of curr dp[i], which is not selecting the current coin, and dp[i - coin] + 1, which is selecting the current coin. Also, we need to make sure i always >= coin

## 💡 Things I have challenges with
1. dp = [float('inf')] * (amount + 1)
2. return dp[-1] if dp[-1] != float('inf') else -1
3. dp[0] = 0

## 🧠 Code
```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        #dp[i] represent to get the current amount, what is the min number of coins to use
        
        dp = [float('inf')] * (amount + 1)
        dp[0] = 0
        
        for i in range(1, amount + 1):
            for coin in coins:
                if i - coin >= 0:
                    dp[i] = min(dp[i], dp[i - coin] + 1)
        
        return dp[-1] if dp[-1] != float('inf') else -1
```

## 📈 Complexity
Time: O(n * amount)
Space: O(n)