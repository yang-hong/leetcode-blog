## 🧩 Problem
https://leetcode.com/problems/daily-temperatures/

## 💭 My thinking process
A monotonic decreasing stack (values decrease from bottom → top). We store Indexes, not temperatures. We want to find, for each day, the next day with a higher temperature. A monotonic decreasing stack guarantees that The temperatures at the stored indexes are strictly decreasing. So when a new temperature T[i] arrives: If T[i] is higher than the stack top, it must be the next warmer day for that index. We pop, update the result, and continue. 

## 💡 Things I have challenges with
1. Increasing stack (1,2,3,4,5-> top) telles the next smaller elements
2. Decreasing stack(5,4,3,2,1 -> top) tells the next larger elements

## 🧠 Code
```
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        res = [0] * len(temperatures)
        stack = [0]

        for i in range(1, len(temperatures)):
            if temperatures[i]<=temperatures[stack[-1]]:
                stack.append(i)
            else:
                while len(stack) > 0 and temperatures[i]>temperatures[stack[-1]]:
                    res[stack[-1]] = i - stack[-1]
                    stack.pop()
                stack.append(i)
        
        return res
```

## 📈 Complexity
Time: O(n)
Space: O(n)