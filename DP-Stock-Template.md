```
dp0 = 今天结束时，不持股的最大利润
dp1 = 今天结束时，持股的最大利润

new_dp0 = max(dp0, dp1 + price - sell_cost)
new_dp1 = max(dp1, dp0 - price - buy_cost)

dp0, dp1 = new_dp0, new_dp1

| 题号  | 限制  | 买入公式 (dp1)                             | 卖出公式 (dp0)                           | 额外状态？ |
| --- | --- | -------------------------------------- | ------------------------------------ | ----- |
| 121 | 一次  | dp1 = -price                           | dp0 = max(dp0, dp1 + price)          | 否     |
| 122 | 无限  | dp1 = max(dp1, dp0 - price)            | dp0 = max(dp0, dp1 + price)          | 否     |
| 309 | 冷冻期 | dp1 = max(dp1, rest - price)           | dp0 = max(dp0, dp1 + price)          | 是     |
| 714 | 手续费 | dp1 = max(dp1, dp0 - price)            | dp0 = max(dp0, dp1 + price - fee)    | 否     |
| 123 | 2 次 | dp1[k] = max(dp1[k], dp0[k-1] - price) | dp0[k] = max(dp0[k], dp1[k] + price) | 否     |
| 188 | K 次 | 同 123                                  | 同 123                                | 否     |

```