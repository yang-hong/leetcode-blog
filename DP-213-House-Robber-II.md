```
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 0:
            return 0
        if n == 1:
            return nums[0]
        
        # 线性版本 House Robber（198）
        def robLinear(arr):
            m = len(arr)
            if m == 0:
                return 0
            if m == 1:
                return arr[0]
            
            dp = [0] * (m + 1)
            dp[1] = arr[0]
            dp[2] = max(arr[0], arr[1])

            for i in range(3, m + 1):
                dp[i] = max(dp[i - 1], dp[i - 2] + arr[i - 1])
            
            return dp[m]
        
        # 情况一：抢第 0 ~ n-2（不抢最后一个）
        case1 = robLinear(nums[:-1])
        
        # 情况二：抢第 1 ~ n-1（不抢第一个）
        case2 = robLinear(nums[1:])
        
        return max(case1, case2)

```