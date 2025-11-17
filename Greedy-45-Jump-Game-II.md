## 🧩 Problem
https://leetcode.com/problems/jump-game-ii/

## 💭 My thinking process
Use a greedy approach: track the farthest index reachable (farthest) and the current jump range (cur_end). As you iterate, update farthest = max(farthest, i + nums[i]). When i == cur_end, it means you’ve reached the end of the current jump range, so increment jumps and set cur_end = farthest. Stop when cur_end reaches or exceeds the last index

## 💡 Things I have challenges with

## 🧠 Code
```
class Solution:
    def jump(self, nums: List[int]) -> int:
        jumps = 0
        cur_end = 0
        farthest = 0
        
        for i in range(len(nums) - 1):  # Don't jump from the last index
            farthest = max(farthest, i + nums[i])
            if i == cur_end:
                jumps += 1
                cur_end = farthest
        
        return jumps

```

## 📈 Complexity
Time: O(n)
Space: O(1)