```
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        n = len(nums)
        res = [-1] * n
        stack = []

        for i in range(2 * n):
            num = nums[i % n]

            while stack and nums[stack[-1]] < num:
                idx = stack.pop()
                res[idx] = num

            # Only push indexes from the first pass
            if i < n:
                stack.append(i)
        
        return res
```