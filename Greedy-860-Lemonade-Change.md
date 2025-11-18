## 🧩 Problem
https://leetcode.com/problems/lemonade-change/

## 💭 My thinking process
There are only 3 condition! when bill is 5, 10, and 20. For bill is 20, we have 2 condition, if there is ten bill, we minus ten, and minus 5. If there is only 5 bill, we minus five 3 times. If whenever five and ten bills becomes less than 0, meaning we don't have any change left, therefore return False

## 💡 Things I have challenges with


## 🧠 Code
```
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        five = 0
        ten = 0

        for bill in bills:
            if bill == 5:
                five += 1
            elif bill == 10:
                ten += 1
                five -= 1
                if five < 0:
                    return False
            elif bill == 20:
                if ten >= 1:
                    ten -= 1
                    five -= 1
                else:
                    five -= 3
                
                if ten < 0 or five < 0:
                    return False
            
        return True
```

## 📈 Complexity
Time: O(n)
Space: O(1)