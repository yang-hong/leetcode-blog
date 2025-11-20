```
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        if not intervals:
            return -1
        
        intervals.sort()
        res = 0
        prev = intervals[0]

        for curr in intervals[1:]:
            #overlap
            if prev[1] > curr[0]:
                #keep the intervals with smaller end time because it is less likely to overlap
                if prev[1] > curr[1]:
                    prev = curr
                res += 1
            else:
                prev = curr
        
        return res

```