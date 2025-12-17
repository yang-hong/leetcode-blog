## 🧩 Problem
https://leetcode.com/problems/permutations-ii/description/

## 💭 My thinking process
For each level of the tree (horizontal), we can always start from the begining, which means just call the recursion without passing any starting_index. We need to track duplicates under each path, because if we won't track, the recursion will always start at index 0, which means it will have so many duplicates like[1,1,1]. Need to take care of the duplication logic

## 💡 Things I have challenges with
1. We need to track duplicates under each path, because if we won't track, the recursion will always start at index 0, which means it will have so many duplicates like[1,1,1]
2. Combination does not have order. Permutation order matters
| 类型 | 所有结果                                     | 总数 |
| -- | ---------------------------------------- | -- |
| 组合 | [1,2], [1,3], [2,3]                      | 3  |
| 排列 | [1,2], [1,3], [2,1], [2,3], [3,1], [3,2] | 6  |

## 🧠 Code
```
class Solution:
    def permuteUnique(self, nums):
        nums.sort()  # 排序
        result = []
        self.backtracking(nums, [], [False] * len(nums), result)
        return result

    def backtracking(self, nums, path, used, result):
        if len(path) == len(nums):
            result.append(path[:])
            return
        for i in range(len(nums)):
            if (i > 0 and nums[i] == nums[i - 1] and not used[i - 1]) or used[i]:
                continue
            used[i] = True
            path.append(nums[i])
            self.backtracking(nums, path, used, result)
            path.pop()
            used[i] = False

```

## 📈 Complexity
| Stage                | Why                                                                    | Cost                 |
| -------------------- | ---------------------------------------------------------------------- | -------------------- |
| Build recursion tree | Each level picks from remaining numbers → n × (n−1) × ... × 1 branches | O(n!)                |
| Copy permutation     | Each full `path` has n elements → copying costs O(n)                   | O(n × n!) total      |
| Recursion stack      | Max depth = n                                                          | O(n) auxiliary space |
