## 🧩 Problem
https://leetcode.com/problems/reverse-string-ii/

## 💭 My thinking process
for each pointer that starts at i, ends at i + k th position, do the swap. and then jump 2k times to get new i

## 💡 Things I have challenges with
1. Origionally it was sliced to array: res[i : i + k] = reverse(res[i : i + k]), so we need to make the res a list and rejoin the list to a string: res = list(s), return ''.join(res)

## 🧠 Code
```
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        # for each pointer that starts at i, ends at i + k th position, do the swap. and then jump 2k times to get new i
        def reverse(n):

            left, right = 0, len(n) - 1
            while left <= right:
                tmp = n[right]
                n[right] = n[left]
                n[left] = tmp
                left += 1
                right -= 1

            return n 

        res = list(s)
        for i in range(0, len(s), 2 * k):
            res[i : i + k] = reverse(res[i : i + k])
        
        return ''.join(res)
                            
```
