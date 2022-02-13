# Summer_Winter Coding(~2018) 배달 (프로그래머스)

문제 - https://programmers.co.kr/learn/courses/30/lessons/12978

```
import heapq

def deliver(N, road, K):
    
    graph = [[] for _ in range(N+1)]
    INF = float('INF')
    distance = [INF] * (N+1)     
    
    for x,y,z in road:
        graph[x].append((y,z))
        graph[y].append((x,z))

    distance[1]=0
    q = []
    heapq.heappush(q, (1, 0))
    
    while q:
        cur, weight = heapq.heappop(q)
        
        if distance[cur] < weight:
            continue
        
        for next, w in graph[cur]:
            total_w = weight + w
            
            if total_w < distance[next]:
                distance[next] = total_w
                heapq.heappush(q, (next, total_w))
    return distance


#road = [[1,2,1],[2,3,3],[5,2,2],[1,4,2],[5,3,1],[5,4,2]] # s, d, w
road = [[1,2,1],[1,3,2],[2,3,2],[3,4,3],[3,5,2],[3,5,3],[5,6,1]]    
N = 6
K = 4
answer=0
res = deliver(N, road, K)

for i in res:
    if i <= 3:
        answer += 1
print(answer)
```
