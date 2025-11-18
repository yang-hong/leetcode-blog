## 🧩 Problem
https://leetcode.com/problems/candy/

## 💭 My thinking process
We do 2 passes. First pass is from left to right, we compare rating[i] with ratings[i - 1]. If ratings[i] is larger, then we plus 1 because the right neighbor needs to be larger. Second pass is from right to left, we compare rating[i] with rating[i + 1], if it is larger, meaning that we have to make the number 1 larger than the right neighbor, so we take the max of curr value or the right neighbor + 1 

## 💡 Things I have challenges with


## 🧠 Code
```
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        candies = [1] * n
        
        # Forward pass: handle cases where right rating is higher than left
        for i in range(1, n):
            if ratings[i] > ratings[i - 1]:
                candies[i] = candies[i - 1] + 1
        
        # Backward pass: handle cases where left rating is higher than right
        for i in range(n - 2, -1, -1):
            if ratings[i] > ratings[i + 1]:
                candies[i] = max(candies[i], candies[i + 1] + 1)
        
        return sum(candies)  

```

## 📈 Complexity
Time: O(n)
Space: O(n)