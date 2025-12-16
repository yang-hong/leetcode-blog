## 🧩 Problem
https://leetcode.com/problems/redundant-connection/description/

## 💭 My thinking process
for each node, we create a parent table with node value, and keep flattening the node using union find until each node reaches its top parent. Find is get the par[x], and equals to find(par[x]) and return. Union is that for edge a to b, find par of a and par of b and append  par b to par a, which is par[pb] = pa. For each edge, if the pa and pb is the same, meaning that they have unioned, so return False and that edge is the edge we want to delete

## 💡 Things I have challenges with
1. rank[pa] > rank[pb], not rank(pa)
2. if not union(x,y): return [x, y]

## 🧠 Code
```
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        par = [i for i in range(len(edges) + 1)]
        rank = [1] * (len(edges) + 1)
        
        def find(x):
            if par[x] != x:
                par[x] = find(par[x])

            return par[x]
            
        def union(a, b):
            pa = find(a)
            pb = find(b)
            if pa == pb:
                return False
            if rank[pa] > rank[pb]:
                par[pb] = pa
                rank[pa] += rank[pb]
            else:
                par[pa] = pb
                rank[pb] += rank[pa]
            return True
        
        for x, y in edges: 
            if not union(x,y):
                return [x, y]
```

## 📈 Complexity
Union-Find with path compression and union-by-rank runs in
O(N α(N)) time and O(N) space.
Because α(N) grows extremely slowly (≤ 5 in the universe),
the operations are effectively O(1).