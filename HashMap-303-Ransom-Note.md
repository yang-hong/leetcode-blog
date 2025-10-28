## 🧩 Problem
https://leetcode.com/problems/ransom-note/

## 💭 My thinking process
create hashmap to store the magazine {letter : frequency}. For each ransomNote, if present in hashmap, -1. if frequency becomes 0, delete the val. If not present, return False

## 💡 Things I have challenges with
1. Grammar remainder: hashmap[c] = hashmap.get(c, 0) + 1

## 🧠 Code
```
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:

        hashmap = defaultdict(int)

        for c in magazine:
            hashmap[c] = hashmap.get(c, 0) + 1
        
        for c in ransomNote:
            if c not in hashmap:
                return False
            else:
                hashmap[c] -= 1
                if hashmap[c] == 0:
                    del hashmap[c]
        
        return True

```