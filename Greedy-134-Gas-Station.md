## 🧩 Problem
https://leetcode.com/problems/gas-station/description/

## 💭 My thinking process
For each station, we calculate the currSum and totalSum by adding gas of this station minus cost of this station. If currSum is less than 0, meaning that we can't reach to the next station starting from this point, so we have to start from the next station and recalcute the currSum. If after the loop, totalSum is still minus 0, meaning that there is no way to reach the end no matter where we start, so we return -1

## 💡 Things I have challenges with


## 🧠 Code
```
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        currSum = 0
        totalSum = 0
        start = 0
        for i in range(len(cost)):
            currSum += gas[i] - cost[i]
            totalSum += gas[i] - cost[i]

            if currSum < 0:
                start = i + 1
                currSum = 0
        
        if totalSum < 0:
            return -1
        
        return start

```

## 📈 Complexity
Time: O(n)
Space: O(1)