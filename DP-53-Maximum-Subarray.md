```
https://leetcode.com/problems/maximum-subarray/description/
最大子数组和 = 以当前位置为结尾的最大连续和（dp[i]）要么延续前面的，要么从自己重新开始。

这句话其实就是 Kadane’s Algorithm（卡丹算法）。

如果 dp[i-1]（前面那段连续数组的和）是正数，那么它能帮你变大 → 继续接着用。

如果 dp[i-1] 是负数，那么它只会拖累你 → 直接舍弃，从 nums[i] 重新开始。

class Solution:
    def maxSubArray(self, nums):
        dp = [0] * len(nums)
        dp[0] = nums[0]
        res = dp[0]

        for i in range(1, len(nums)):
            dp[i] = max(nums[i], dp[i-1] + nums[i])
            res = max(res, dp[i])
        
        return res
```