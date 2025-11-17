## 🧩 Problem
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

## 💭 My thinking process
We can use greedy, which is only taking the part of optimal instead of the whole picture. We have another table calculate each days's profit, starting from day2. If the curr day and prev day has positive value, meaning it is making money, so we add that to our final result

## 💡 Things I have challenges with
1. We only add the final value to the result!
2. result += max(prices[i] - prices[i - 1], 0) this will also adding the positive value only! We only take the number that is larger than 0. If it is not, add 0

## 🧠 Code
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = [0]
        res = 0

        for i in range(len(prices)):
            if i > 0:
                day_profit = prices[i] - prices[i - 1]
                profit.append(day_profit)
        
        for i in range(len(profit)):
            if profit[i] > 0:
                res += profit[i]
        
        return res

```

## 📈 Complexity
Time: O(n)
Space: O(n)
