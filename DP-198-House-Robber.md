## 🧩 Problem
https://leetcode.com/problems/house-robber/

## 💭 My thinking process
We can pick or not pick the current house. we take the maximum amount of pick of not pick for ith number of house. If not pick, should be dp[i - 1], which is the previous house. dp[i] = max money robbed from house 0 to house i

## 💡 Things I have challenges with
1. dp[0] = nums[0] !! not 0, dp[1] = max(nums[0], nums[1]), not max(0, 1)!! not max(1,2), nums[0] means the first house
2. we have to initialize dp[] the same size as nums, or else it will have out of index error

## 🧠 Code
```
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 0:
            return 0
        if n == 1:
            return nums[0]
        
        # dp[i] = max money robbed from house 0 to house i
        dp = [0] * n
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])

        for i in range(2, n):
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

        print(dp)
        return dp[-1] 
```

## 📈 Complexity
Time: O(n)
Space: O(n)