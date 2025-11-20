## 🧩 Problem
https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/

## 💭 My thinking process
First, sort ballons based on the start position. After sorting, we need to find the anchor line where we plan to shot the arrow and keep updating that. There are two conditions, if i-1 last position (curr_min_right) is less than start position of i, meaning that there is no overlap, so we have to increase the result, and then update the new anchor to last position of i. If there is overlap, we update the anchor based on the smallest right of i and i - 1

## 💡 Things I have challenges with

## 🧠 Code
```
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        if len(points) == 0:
            return 0

        points.sort(key=lambda x: x[0])

        curr_min_right = points[0][1]
        count = 1
        for i in points:
            #no overlap, increase the count and update the curr_min_right
            if i[0] > curr_min_right:
                count += 1
                curr_min_right = i[1]
            else:
                #overlap, update the curr_min_right based on the smallest right of these 2 intervals for new anchor point
                curr_min_right = min(curr_min_right, i[1])
        
        return count
```

## 📈 Complexity
Time: O(nlogn)
Space: O(1)