## 🧩 Problem
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/

## 💭 My thinking process
There are three states: hold(buy or keep holding), sell, rest. Set the initial hold as price[0], hold and sell as 0. Loop through each day, for each day, make the curr status as previous status, and make hold, sale, rest equal to the transaction function. Hold is the max of previous hold and pre rest - price[i]. Sell is prev hold + price. Rest is max of prev rest and prev sold 

## 💡 Things I have challenges with
1. Transaction function:             hold = max(prev_hold, prev_rest - price)
            sold = prev_hold + price
            rest = max(prev_rest, prev_sold)
2. No need 2D dp table. Though when illustrating case we need to have table with x = day and y = each status

## 🧠 Code
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices:
            return 0
        
        n = len(prices)
        hold = -prices[0]
        sold = 0
        rest = 0

        for i in range(n):
            price = prices[i]
            prev_hold = hold
            prev_sold = sold
            prev_rest = rest

            hold = max(prev_hold, prev_rest - price)
            sold = prev_hold + price
            rest = max(prev_rest, prev_sold)
        
        return max(sold, rest)
```

## 📈 Complexity
Time: O(n)
Space: O(1)