```
#https://leetcode.com/problems/min-cost-climbing-stairs/description/
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        # dp[i] = minimum cost to reach step i
        n = len(cost)
        dp = [0] * n
        dp[0] = cost[0]
        dp[1] = cost[1]

        for i in range(2, n):
            dp[i] = cost[i] + min(dp[i-1], dp[i-2])
        
        print(dp)
        print(n)
        print(dp[n-1])
        return min(dp[n-1], dp[n-2])
```