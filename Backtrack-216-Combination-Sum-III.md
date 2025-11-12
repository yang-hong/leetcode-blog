```
#https://leetcode.com/problems/combination-sum-iii/description/
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        res = []
        path = []

        def backtrack(start, remain):
            if len(path) == k and remain == 0:
                res.append(path[:])
                return
            
            if len(path) > k and remain < 0:
                return 
            
            for i in range(start, 10):
                path.append(i)
                backtrack(i + 1, remain - i)
                path.pop()
        
        backtrack(1, n)
        return res
```