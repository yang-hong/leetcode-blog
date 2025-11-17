## 🧩 Problem
https://leetcode.com/problems/jump-game/description/

## 💭 My thinking process
We can use greedy, which is only taking the part of optimal instead of the whole picture. We want to have a cover variable that keeps track the maximum position we can reach. All the coverage under that maximum position is reachable. Until we find out that there is a position we can't reach (when i > cover), we return False. Otherwise, return true

## 💡 Things I have challenges with
1. if i <= cover
2. cover = max(i + nums[i], cover)

## 🧠 Code
```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        if len(nums) == 1:
            return True
        
        cover = 0
        i = 0
        for i in range(len(nums)):
            if i <= cover:
                cover = max(i + nums[i], cover)
                if cover >= len(nums) - 1:
                    return True
        
        return False

```

## 📈 Complexity
Time: O(n)
Space: O(1)