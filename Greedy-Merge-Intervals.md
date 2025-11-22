## 🧩 Problem
https://leetcode.com/problems/merge-intervals/

## 💭 My thinking process
Have a tmp variable initialized to first element to track if it is ok to put the tmp to result. If there is an overlap between tmp and curr variable, we merge these 2 invals to tmp, and keep comparing this tmp to the next curr, if there is still overlap, we keep merging to tmp, if there is no overlap, we can finally put the tmp to result, and move to the next elements for comparison (move tmp to curr). After for loop ends, put the last element(tmp) to res

## 💡 Things I have challenges with
1. tmp[1] = max(tmp[1], i[1])! we need to write tmp[1] instead of tmp
2. if tmp[1] >= i[0], there is an equal sign because when tmp end and curr start equals, there is still overlap
3. tmp = i instead of tmp == i!

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