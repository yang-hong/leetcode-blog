## 🧩 Problem
https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/description/

## 💭 My thinking process
Sort the nums so negative comes first. For each negative, we times -1 to make it positive and minus k. If k is still larger than 0, meaning there are still flips we need to do. We only care about if k is odd number because if it is even number, we can flip any number 2 times, which will not change the result. If it is odd number, we resort the number, now the first number is smallest, so we just need to change sign of that number, and we add all nums from number list

## 💡 Things I have challenges with
1. Add all numbers from list: sum(nums)
2. Find if it is odd: k % 2 = 1
3. Find the smallest number: we re-sort the number list after negative sign has been flipped to positive

## 🧠 Code
```
class Solution:
    def largestSumAfterKNegations(self, nums: List[int], k: int) -> int:
        nums.sort()

        for i in range(len(nums)):
            if k > 0 and nums[i] < 0:
                nums[i] = -nums[i]
                k -= 1
            
        if k % 2 == 1:
            nums.sort()
            nums[0] = -nums[0]
        
        return sum(nums)

```

## 📈 Complexity
Time: O(n log n) (sorting dominates)
Space: O(1)