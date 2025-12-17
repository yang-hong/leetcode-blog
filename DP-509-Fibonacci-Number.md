## 🧩 Problem
https://leetcode.com/problems/merge-intervals/

## 💭 My thinking process
Transaction function: dp[i] = dp[i - 1] + dp[i - 2]

## 💡 Things I have challenges with
1. dp table length should be n + 1  instead of n! 
2. dp table: dp = [0] * n + 1
3. Base case check: dp[0] + dp[1]

## 🧠 Code
```
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        res = []

        tmp = intervals[0]
        for i in intervals[1:]:
            #overlap, expand the tmp interval
            if tmp[1] >= i[0]:
                 tmp[1] = max(tmp[1], i[1])
            else:
                res.append(tmp)
                tmp = i
        res.append(tmp) #must append the last interval
        return res
```

## 📈 Complexity
Time: O(n)
Space: O(n)