## 🧩 Problem
https://leetcode.com/problems/3sum/

## 💭 My thinking process
Use three pointer. Sort the list first. Loop through first pointer, and under that for loop, set left and right pointer and calculate the sum of three pointer. If it is larger than 0, narrow down to the left

## 💡 Things I have challenges with
1. For left and right pointer, it is purely two pointer, but not binary search! so it has to be right -= 1 instead of mid
2. Left pointer should be i + 1 instead of 1 or 0 to avoid duplicate
3. while left <= right: should be while left < right to avoid duplicate
4. Should be res.append after finding pair, not return res.append to avoid existing the program early
5. For duplicate handling, should consider both outer loop and inner loop

## 🧠 Code
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()

        for i in range(len(nums)):
            left, right = i + 1, len(nums) - 1

            #skip outter loop duplicate
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            while left < right:
                total = nums[left] + nums[right] + nums[i]
                
                if total > 0:
                    right -= 1
                elif total < 0:
                    left += 1
                else:
                    res.append([nums[i], nums[left], nums[right]])
                    left += 1
                    right -= 1
                    while left < right and nums[left] == nums[left - 1]:
                        left += 1
                    while left < right and nums[right] == nums[right + 1]:
                        right -= 1
        
        return res
```

## 📈 Complexity
| Operation          | Complexity               | Reason                    |
| ------------------ | ------------------------ | ------------------------- |
| Sorting            | O(n log n)               | Timsort                   |
| Outer loop         | O(n)                     | Fix each number           |
| Two-pointer search | O(n) per outer iteration | Left/right move once each |
| **Total time**     | **O(n²)**                | Dominated by double loop  |
| **Space**          | **O(1)**                 | Constant extra variables  |
