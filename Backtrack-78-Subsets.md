## 🧩 Problem
https://leetcode.com/problems/subsets/description/

## 💭 My thinking process
Because this is subsets, unlike combination that only returns the leaf results, it has to return all the node's result. Horizontal tree is each number from index0 to the last index. Vertical tree is the next numbeer from start index. For each vertical node, we put the number to path (without return). For each node, we return the path immediately to result

## 💡 Things I have challenges with
1. Because [] is also counted, before entering the recursion and for loop, we need to append the path to result. ALways to shallow copy
2. WHen we call recursion, it is backtrack(nums, 0, path, res) instead of backtrack(nums, 0, [], []). In python, it is pass by reference. [] will initialize a new object, which will not pass to the recursion

## 🧠 Code
```
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        path = []

        def backtrack(nums, start_index, path, res):
            res.append(path[:])

            for i in range(start_index, len(nums)):
                path.append(nums[i])
                backtrack(nums, i + 1, path, res)
                path.pop()
        
        backtrack(nums, 0, path, res)
        return res

```

## 📈 Complexity
| Component               | Complexity | Explanation                            |
| ----------------------- | ---------- | -------------------------------------- |
| **Time**                | O(n × 2ⁿ)  | Explore all subsets + copy each subset |
| **Space (Auxiliary)**   | O(n)       | Max recursion depth                    |
| **Total (with output)** | O(n × 2ⁿ)  | Size of all subsets stored             |
