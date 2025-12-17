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
