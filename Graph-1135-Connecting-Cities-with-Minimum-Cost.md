## 🧩 Problem
https://leetcode.com/problems/connecting-cities-with-minimum-cost/

## 💭 My thinking process
“Prim’s algorithm grows the minimum spanning tree by always selecting the minimum-weight edge that connects a visited node to an unvisited node. Build a adjacency list and use minHeap. Start from any node, mark it as visited, and push all its outgoing edges into a min-heap. Repeatedly extract the minimum-weight edge from the heap; if it connects to an unvisited node, add that node to the tree and push its edges into the heap. Continue until all nodes are visited; the sum of selected edge weights is the minimum spanning tree cost (otherwise the graph is disconnected).

## 💡 Things I have challenges with
1. for u, v, w in connections:
            u -= 1
            v -= 1
    because node start at 1 instead of 0

## 🧠 Code
```
class Solution:
    def minimumCost(self, n: int, connections: List[List[int]]) -> int:
        graph = [[] for _ in range(n)]

        for u, v, w in connections:
            u -= 1
            v -= 1
            graph[u].append((v, w))
            graph[v].append((u, w))
        print(graph)

        visited = [False] * n
        min_heap = [(0,0)]
        total = 0
        count = 0

        #prim
        while min_heap and count < n:
            cost, u = heapq.heappop(min_heap)

            if visited[u]:
                continue
            
            visited[u] = True
            total += cost
            count += 1

            for v, w in graph[u]:
                if not visited[v]:
                    heapq.heappush(min_heap, (w, v))
        
        return total if count == n else -1

```

```
二、Kruskal 算法 3 步总结

将所有边按权重从小到大排序

依次取边，用并查集判断两端是否已经连通

不连通就合并并计入成本，直到选够 n - 1 条边

class Solution:
    def minimumCost(self, n: int, connections: List[List[int]]) -> int:
        # 1. 并查集初始化（0-based）
        parent = [i for i in range(n)]
        rank = [1] * n

        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])   # 路径压缩
            return parent[x]

        def union(a, b):
            pa, pb = find(a), find(b)
            if pa == pb:
                return False                 # 会成环
            if rank[pa] < rank[pb]:
                parent[pa] = pb
                rank[pb] += rank[pa]
            else:
                parent[pb] = pa
                rank[pa] += rank[pb]
            return True

        # 2. 边排序（1-based → 0-based）
        connections.sort(key=lambda x: x[2])

        total = 0
        edges_used = 0

        # 3. 逐边尝试合并
        for u, v, cost in connections:
            u -= 1
            v -= 1
            if union(u, v):
                total += cost
                edges_used += 1
                if edges_used == n - 1:
                    return total

        return -1

```

## 📈 Complexity
Time Complexity:
O(E log V)

Each edge can be pushed into the heap

Each heap operation costs log V

Space Complexity:
O(E + V)

Adjacency list stores all edges

Heap can contain up to E edges

visited array stores V nodes
