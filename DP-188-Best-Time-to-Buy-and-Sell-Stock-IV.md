```
一次交易 = 买 → 卖
K 次交易 = 买卖买卖...买卖（共 2K 个状态）
dp[j] 存储第 j 状态的最大利润
奇数是买，偶数是卖

class Solution:
    def maxProfit(self, K: int, prices: List[int]) -> int:
        n = len(prices)
        if n == 0 or K == 0:
            return 0
        
        # 如果 K 很大，相当于无限次交易（退化成 122）
        if K > n // 2:
            profit = 0
            for i in range(1, n):
                if prices[i] > prices[i-1]:
                    profit += prices[i] - prices[i-1]
            return profit
        
        dp = [-float('inf')] * (2*K + 1)
        dp[0] = 0
        dp[1] = -prices[0]

        for price in prices:
            for j in range(1, 2*K + 1):
                if j % 2 == 1:    # buy
                    dp[j] = max(dp[j], dp[j-1] - price)
                else:             # sell
                    dp[j] = max(dp[j], dp[j-1] + price)
        
        return dp[2*K]

```