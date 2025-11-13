
## 🧩 Problem
https://leetcode.com/problems/combination-sum-ii/description/

## 💭 My thinking process
Each number in candidates may only be used once in the combination, meaning that you can't reuse the numbers in one combination, so in the recursion, we need to have i + 1. Also, find all unique combinations in candidates, meaning that in the horizontal tree, if candidates[i] == candidates[i - 1], we skip

## 💡 Things I have challenges with
1. Need to sort the candidates first to eliminate the duplicates from horizontal tree
2. if i > curr and candidates[i] == candidates[i - 1] to avoid out of boundary
3. backtrack(i + 1, candidates, path, remain - candidates[i]) instead of target - candidates[i]

## 🧠 Code
```
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
            
        res = []
        number_to_letters = {
            "2" : "abc",
            "3" : "def",
            "4" : "ghi",
            "5" : "jkl",
            "6" : "mno",
            "7" : "pqrs",
            "8" : "tuv",
            "9" : "wxyz"
        }

        def backtrack(curr_index, path):
            if curr_index == len(digits):
                res.append(path[:])
                return
            
            curr_number = digits[curr_index]
            curr_letters = number_to_letters[curr_number]
            
            for curr_letter in curr_letters:
                backtrack(curr_index + 1, path + curr_letter)
            
        backtrack(0, "")
        return res
```