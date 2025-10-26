## 🧩 Problem
https://leetcode.com/problems/intersection-of-two-arrays/

## 💭 My thinking process
Create a set to put numbers from nums1. Loop through numbers from nums2, if we see the same value from set, put to the result. 

## 💡 Things I have challenges with
1. Because there should be no duplicate, so the result should not be array (it will include duplicate from nums2). It should be set to eliminate duplicate
2. Return type is list. So we need to return list(res)

## 🧠 Code
```
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        seen = set(nums1)
        res  = set()

        for n in nums2:
            if n in seen:
                res.add(n)
        
        return list(res)

```