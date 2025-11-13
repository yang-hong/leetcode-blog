## 🧩 Problem
https://leetcode.com/problems/palindrome-partitioning/

## 💭 My thinking process
The horizontal tree is like we cut at i th place, and vertical tree is like for ith place, add one more element down. For each path generated, we need another function to tell if it is palindrome

## 💡 Things I have challenges with

## 🧠 Code
```
class Solution:
    def isPalindrome(self, subs):
        return subs == subs[::-1]

    def partition(self, s: str) -> List[List[str]]:
        res = []

        def backtrack(start, path):
            if start == len(s):
                res.append(path[:])
                return
            
            for end in range(start, len(s)):
                if self.isPalindrome(s[start:end+1]):
                    path.append(s[start:end+1])
                    backtrack(end + 1, path)
                    path.pop()
        
        backtrack(0,[])
        return res
```

## 📈 Complexity
| Metric             | Complexity     | Explanation                                           |
| ------------------ | -------------- | ----------------------------------------------------- |
| **Time (no DP)**   | O(n × 2ⁿ)      | Explore all partitions, check palindrome in O(n) each |
| **Time (with DP)** | O(n² + n × 2ⁿ) | Precompute palindromes + backtrack                    |
| **Space (aux)**    | O(n²)          | DP table + recursion stack                            |
| **Result size**    | O(n × 2ⁿ)      | All valid partitions                                  |
