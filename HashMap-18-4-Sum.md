## 🧩 Problem
https://leetcode.com/problems/4sum/

## 💭 My thinking process
Like 3 sum, but need to take care of the negative value because the total is not 0, it is target. Use nested for loop

## 💡 Things I have challenges with
1. With the range for for loop, for i in range(n - 3), for j in range(i + 1, n -2)
2. Each level need duplication logic. 
    1. First level: if i > 0 and nums[i] == nums[i - 1]: continue
    2. Second level: if j > i + 1 and nums[j] == nums[j - 1] : continue
    3. Third level: while l < r and nums[l] == nums[l + 1] : l += 1, while l < r and nums[r] < nums[r - 1]: r -= 1
3. With above duplication logic, we need to write duplication logic at first, and then move the left and right pointer (l += 1, r += 1)

## 🧠 Code
```
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        res = []
        n = len(nums)

        for i in range(n - 3):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            for j in range(i + 1, n - 2):
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue
                l, r = j + 1, n - 1
                while l < r:
                    current_sum = nums[i] + nums[j] + nums[l] + nums[r]
                    if current_sum < target:
                        l += 1
                    elif current_sum > target:
                        r -= 1
                    else:
                        res.append([nums[i], nums[j], nums[l], nums[r]])
                        while l < r and nums[l] == nums[l + 1]:
                            l += 1
                        while l < r and nums[r] == nums[r - 1]:
                            r -= 1
                        l += 1
                        r -= 1
        return res
                            
```

## 📈 Complexity
| Step               | Operation     | Complexity |
| ------------------ | ------------- | ---------- |
| Sorting            | `nums.sort()` | O(n log n) |
| Two outer loops    | Choose (i, j) | O(n²)      |
| Two-pointer search | per (i, j)    | O(n)       |
| **Total**          |               | **O(n³)**  |
| **Space**          |               | **O(1)**   |

