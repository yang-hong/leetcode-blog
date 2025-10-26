## 🧩 Problem
https://leetcode.com/problems/valid-anagram/description/

## 💭 My thinking process
Create map to store the character as key and frequence as value

## 💡 Things I have challenges with
1. Need to create 2 maps, so that we can compare these 2 maps to see if they are similar
2. Add corner case. If the length of 2 strings are already different, meaning these 2 strings are different. We return False directly
3. Creating map, defaultdict(), we need to specify value type. In this case, defaultdict(int)

## 🧠 Code
```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        s_dict = defaultdict(int)
        t_dict = defaultdict(int)

        #edge case
        if len(s_dict) != len(t_dict):
            return False

        for i in s:
            s_dict[i] += 1
        
        for j in t:
            t_dict[j] += 1
        
        return s_dict == t_dict

```