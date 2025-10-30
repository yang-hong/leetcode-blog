## 🧩 Problem
https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/

## 💭 My thinking process
Start with first index of haystack to the lengh of needle, compare the substring with needle string. If not match, move tto the second index

## 💡 Things I have challenges with
1. Don't compare individual character, it will not work
2. Optimization solution is to use prefix sum
3. for i in range(len(haystack) - len(needle) + 1). Should add 1

## 🧠 Code
```
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if len(needle) > len(haystack):
            return -1
        if not needle: 
            return -1

        for i in range(len(haystack) - len(needle) + 1):
            if haystack[i : i + len(needle)] == needle:
                return i
        
        return -1

```

## 📈 Complexity
Time Complexity

O((n - m + 1) * m) in worst case
(n = len(haystack), m = len(needle))

O(1) extra space