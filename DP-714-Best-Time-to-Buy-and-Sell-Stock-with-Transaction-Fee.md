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

## 📈 Complexity
Time: O(n)
Space: O(1)