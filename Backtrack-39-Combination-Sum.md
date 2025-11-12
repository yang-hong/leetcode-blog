
## 🧩 Problem
https://leetcode.com/problems/combination-sum/

## 💭 My thinking process
For backtrack, because in the vertical tree, we can use the same number, so for each recursion, we can always start with the starting point, which is i. For horizontal, we need to keep increasing the i, so the range is [curr, len(candidates)]. When remain is equal to 0, we append the path and return

## 💡 Things I have challenges with
1. Need to do path.pop() for backtrack!!!
2. Can't use target and update target directly. Because target is a fixed number for each recursion. So, we need to use remain
3. if remain < 0, return

## 🧠 Code
```
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []

        def backtrack(curr, path, remain):
            if remain == 0:
                res.append(path[:])
                return
            
            if remain < 0:
                return
            
            for i in range(curr, len(candidates)):
                path.append(candidates[i])
                backtrack(i, path, remain - candidates[i])
                path.pop()
                
        backtrack(0, [], target)
        return res
```

## 📈 Complexity
在“组合类”或“子集类”回溯题中（如 Subset Sum、Combination Sum、Permutations），一个常见的通用上界是 O(2ⁿ)：

每个元素都有两种决策：选 or 不选 → 一共 2ⁿ 种状态。

每个状态都可能调用一次递归或进入一次分支。

每个分支可能会做 O(n) 的处理（比如遍历 candidates）。

时间复杂度：O(n × 2ⁿ)

递归栈深度 ≈ target / min(candidate) → 记作 O(target)。

因为每次递归都在减小剩余值 remain，最多递归 target 次。
空间复杂度：O(target)
