## 🧩 Problem
https://leetcode.com/problems/palindromic-substrings/description/

## 💭 My thinking process
dp[i][j] = True if s[i + 1][j - 1] is palindrome. So Need to fill the dp table from bottom right. If dp[i] == dp[j] and j - i <= 1, we return True directly. If it is more than 2 character aways, we need to validate if the characters in between is also palindrome, which is using if s[i + 1][j - 1] is true, we return true. This is different from the two pointer solution, for 2 pointer, we take i as the center of palindrom and expand

## 💡 Things I have challenges with
1. should be dp[i][j]!!! shouldn't be s[i][j]
2. = instead of == 

## 🧠 Code
```
class Solution:
    def countSubstrings(self, s: str) -> int:
        #dp[i][j] = True if s[i + 1][j - 1] is palindrome. So Need to fill the dp table from bottom right
        n = len(s)
        dp = [[False] * n for _ in range(n)]
        result = 0

        for i in range(len(s) - 1, -1, -1):
            for j in range(i, len(s)):
                if s[i] == s[j]:
                    if j - i <= 1: #case 1 and2: aa or a
                        result += 1
                        dp[i][j] = True
                    else: #case3. aaa or more
                        if dp[i + 1][j - 1] == True:
                            result += 1
                            dp[i][j] = True
                else:
                    dp[i][j] = False

        return result
```

```
class Solution:
    def countSubstrings(self, s: str) -> int:
        result = 0
        for i in range(len(s)):
            result += self.extend(s, i, i, len(s)) #以i为中心
            result += self.extend(s, i, i+1, len(s)) #以i和i+1为中心
        return result
    
    def extend(self, s, i, j, n):
        res = 0
        while i >= 0 and j < n and s[i] == s[j]:
            i -= 1
            j += 1
            res += 1
        return res
```

## 📈 Complexity
Time: O(n*n)
Space: O(n*n), for 2 pointer, O(1)