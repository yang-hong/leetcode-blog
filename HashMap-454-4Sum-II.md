## 🧩 Problem
https://leetcode.com/problems/4sum-ii/

## 💭 My thinking process
For each value in nums1 and nums2, create a hashmap to store {n1 + n2 : frequency}. For each value in nums3 and nums4, if -(n3 + n4) present in frequency map, result += frequency of that value

## 💡 Things I have challenges with
1. Result should not only += 1, it should += frequency value because we don't want to eliminate the duplicate
2. If n1 + n2 + n3 + n4 == 0, n1 + n2 has to equals to - (n3 + n4)

## 🧠 Code
```
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        hashmap = defaultdict(int)
        res = 0

        for a in nums1:
            for b in nums2:
                total = a + b
                hashmap[total] = hashmap.get(total, 0) + 1
        
        for c in nums3:
            for d in nums4:
                total = - (c + d)
                if total in hashmap:
                    res += hashmap[total]
        
        return res

```

## 📈 Complexity
| Measure   | Explanation                          | Complexity |
| --------- | ------------------------------------ | ---------- |
| **Time**  | Two nested loops for each pair group | **O(n²)**  |
| **Space** | Hash map stores all (a+b) sums       | **O(n²)**  |
