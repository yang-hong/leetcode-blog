```
01背包理论基础 (opens new window)，中二维DP数组的递推公式为：

dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i])

在 完全背包理论基础 (opens new window)详细讲解了完全背包二维DP数组的递推公式为：

dp[i][j] = max(dp[i - 1][j], dp[i][j - weight[i]] + value[i])

class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 1

        for coin in coins:
            for i in range(coin, amount + 1):
                dp[i] += dp[i - coin]
        
        print(dp)
        return dp[amount]
```