## 🧩 Problem
https://leetcode.com/problems/assign-cookies/

## 💭 My thinking process
We sort the cookie and children first. We also has a children index to count how many children can eat. For each cookie, if it is larger than children, meaning we can give to this children, so we add children index

## 💡 Things I have challenges with
1. Sort the list: s_sorted = sorted(s)
2. We need to use the sorted vaiable, which is s_sorted

## 🧠 Code
```
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        sorted_g = sorted(g)
        sorted_s = sorted(s)

        children_index = 0
        for i in range(len(sorted_s)):
            if children_index < len(sorted_g) and sorted_g[children_index] <= sorted_s[i]:
                children_index += 1
        
        return children_index
```