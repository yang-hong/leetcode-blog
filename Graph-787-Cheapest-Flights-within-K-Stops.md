## 🧩 Problem
https://leetcode.com/problems/cheapest-flights-within-k-stops/

## 💭 My thinking process
Bellman-Ford relaxes edges step by step

Initialize distances:

dist[src] = 0

all others = infinity

Repeat K + 1 times:

Relax all edges

Use a copy of the previous distance array

Take the minimum distance to the destination

## 💡 Things I have challenges with

## 🧠 Code
```
class Solution:
    def findCheapestPrice(self, n, flights, src, dst, k):
        INF = float('inf')
        dist = [INF] * n
        dist[src] = 0

        # 最多 k+1 条边 → 松弛 k+1 轮
        for _ in range(k + 1):
            new_dist = dist[:]  # 必须复制！
            for u, v, w in flights:
                if dist[u] == INF:
                    continue
                if dist[u] + w < new_dist[v]:
                    new_dist[v] = dist[u] + w
            dist = new_dist

        return dist[dst] if dist[dst] != INF else -1

```

```
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, k: int) -> int:
        #step1: build adjacent list [key(src): values((desc, cost))]
        graph = defaultdict(list)
        for u, v, price in flights:
            graph[u].append((v, price))
        print(graph)

        #queue for bfs: (curr_cost, curr_city, curr_steps)
        queue = deque()
        queue.append((0, src, 0))

        #lists for both curr_distance and curr_steps(stops) 
        dist = [float('inf')] * n
        stops = [float('inf')] * n
        dist[src] = 0
        stops[src] = 0

        #bfs
        while queue:
            cost, city, step = queue.popleft()

            if step > k:
                continue
            
            for neighbor, price in graph[city]:
                new_cost = price + cost
                if new_cost < dist[neighbor] or step < stops[neighbor]:
                    dist[neighbor] = new_cost
                    stops[neighbor] = step
                    queue.append((new_cost, neighbor, step + 1))
        
        return dist[dst] if dist[dst] != float('inf') else -1

```

## 📈 Complexity