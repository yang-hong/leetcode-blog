```
✔ 1. Coin Change II（518）算“组合”（顺序不重要）

→ 外层 coin
→ 内层金额
→ j 从 coin 开始
→ dp[j] += dp[j - coin]

✔ 2. Combination Sum IV（377）算“排列”（顺序重要）

→ 外层金额（j）
→ 内层 nums
→ 所有顺序都被统计

✔ 3. 为什么答案变多？

因为：

1 + 3 和 3 + 1 算不同序列
```

```
🌟 j=3：

num=1: dp[3] += dp[2] = 2

num=2: dp[3] += dp[1] = 1

num=3: dp[3] += dp[0] = 1

dp = [1,1,2,4,0]


方案：

1+1+1
1+2
2+1
3
```

```
class Solution:
    def combinationSum4(self, nums, target):
        dp = [0] * (target + 1)
        dp[0] = 1
        
        for j in range(1, target + 1):        # 金额在外层（顺序敏感）
            for num in nums:                 # 数字在内层（顺序 matters）
                if j >= num:
                    dp[j] += dp[j - num]
        
        return dp[target]

```