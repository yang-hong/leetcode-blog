## 🧩 Problem
https://leetcode.com/problems/two-sum/

## 💭 My thinking process
Create a dictionary [value : index]. For each index, calculate its remaining. If it does not exist in the dictionary, add the remaining and index to dictionary, else return [remaining index, curr index]

## 💡 Things I have challenges with
1. dictionary: [value : index]
2. when adding to dictionary: nums_dict[nums[i]] = i, it should be nums[i] instead of remaining because we need to add the current index

## 🧠 Code
```
class Solution:
    def isHappy(self, n: int) -> bool:
        seen = set()

        while n > 1:
            #process the endless loop case
            if n in seen: 
                return False
            seen.add(n)

            total = 0
            while n > 0:
                digit = n % 10
                total += digit * digit
                n = n // 10
            
            n = total # reset n to new total after all the current digits are processed
        
        return True

```