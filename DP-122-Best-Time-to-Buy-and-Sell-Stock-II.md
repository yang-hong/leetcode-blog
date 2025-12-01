https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = [0]
        res = 0

        for i in range(len(prices)):
            if i > 0:
                day_profit = prices[i] - prices[i - 1]
                profit.append(day_profit)
        print(profit)
        
        for i in range(len(profit)):
            if profit[i] > 0:
                res += profit[i]
        
        return res
```

```
class Solution:
    def maxProfit(self, prices):
        dp0 = 0
        dp1 = -prices[0]

        for price in prices[1:]:
            new_dp0 = max(dp0, dp1 + price)
            new_dp1 = max(dp1, dp0 - price)
            dp0, dp1 = new_dp0, new_dp1
        
        return dp0
```