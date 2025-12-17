## 🧩 Problem
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/

## 💭 My thinking process
There are 2 status. Sell and buy. For each day, if sell, price is equal to max of previous day's sale (not selling today), and prev buy + today's price - fee. If buy, price is max of previous day's buy and previous day's sale - price 

## 💡 Things I have challenges with
1. If set variable sale as prev sale, the curr day's sale should be new_sale. After that, set sale equal to new_sale

## 🧠 Code
```
class Solution:
    def maxProfit(self, prices: List[int], fee: int) -> int:
        sell = 0
        buy = -prices[0]

        for price in prices[1:]:
            new_sell = max(sell, buy + price - fee)
            new_buy = max(buy, sell - price)
            sell, buy = new_sell, new_buy
        return sell
```

```
class Solution:
    def maxProfit(self, prices, fee):
        n = len(prices)

        # dp0 = 结束时手里没有股票的最大利润
        # dp1 = 结束时手里持有股票的最大利润
        dp0 = 0                 # 不持股
        dp1 = -prices[0]        # 持股（第0天买的话的初始状态）

        for i in range(1, n):
            price = prices[i]

            # 保存前一天的 dp 状态
            prev_dp0 = dp0
            prev_dp1 = dp1

            # 今天结束时不持股 = 昨天不持股 或 昨天持股今天卖掉（扣 fee）
            dp0 = max(prev_dp0, prev_dp1 + price - fee)

            # 今天结束时持股 = 昨天持股 或 昨天不持股今天买入
            dp1 = max(prev_dp1, prev_dp0 - price)

        return dp0
```

## 📈 Complexity
Time: O(n)
Space: O(1)