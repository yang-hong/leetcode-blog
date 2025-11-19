## 🧩 Problem
https://leetcode.com/problems/queue-reconstruction-by-height/description/

## 💭 My thinking process
First, sort people based on height (from tall to short). If they have the same height, sort by k(from low to high), this is to make sure tall are not interrupt by the short. After sort, we loop through all people, and insert to result array based on k's position. Because we already sorted from tall to short, the insert position already make sure that there is no people that is taller than us after that 

## 💡 Things I have challenges with
1. Sort by lambda. people.sort(key=lambda x:(-x[0], x[1]))
2. Insert to array by position: res.insert(p[1], p)

## 🧠 Code
```
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        people.sort(key=lambda x: (-x[0], x[1]))

        res = []
        for p in people:
            res.insert(p[1], p)
        
        return res
```

## 📈 Complexity
Time: O(nlogn)
Space: O(n)