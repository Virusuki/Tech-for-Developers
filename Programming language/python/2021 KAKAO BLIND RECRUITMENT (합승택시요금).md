# 합승 택시 요금 (최단거리알고리즘)

- 문제 : https://programmers.co.kr/learn/courses/30/lessons/72413

```
def dijkstra(start, arrive):
    
    INF = float('INF')
    distance = [INF]*(N+1)
    
    q=[]
    
    heapq.heappush(q, (start, 0))
    
    while q:
        dist, weight = heapq.heappop(q)
        
        if distance[dist] < weight:
            continue
        
        for v, w in graph[dist]:
            total_w = weight + w
            
            if total_w < distance[v]:
                distance[v] = total_w
                heapq.heappush(q, (v, total_w))
    
    return distance[arrive]
 
n = 6
s = 4
a = 6
b = 2
fares = [[4, 1, 10], [3, 5, 24], [5, 6, 2], [3, 1, 41], [5, 1, 24], [4, 6, 50], [2, 4, 66], [2, 3, 22], [1, 6, 25]]    
    
global graph, N
graph=[]
N=n

graph = [[] for i in range(n+1)]

for i,j,k in fares:
    graph[i].append((j,k))
    graph[j].append((i,k))

INF = float("INF")
total_weight = INF

# shortest node
for sn in range(N):
    total_weight = min(total_weight, dijkstra(sn, s) + dijkstra(sn, a) + dijkstra(sn, b))

print(total_weight)
```
