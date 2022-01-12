
- DFS 깊이우선탐색 
```
def dfs_recur(v, discovered=[]):
    
    graph ={
    1:[2,3,4],
    2:[5],
    3:[5],
    4:[],
    5:[6,7],
    6:[],
    7:[3]
    }
    
    discovered.append(v)
    
    for i in graph[v]:  # i번째의 정점에서 인접 간섭을 방문 
        if i not in discovered:   # 만약 discovered 변수에 인접점들이 없다면 저장을 위해 순회
            discovered=dfs_recur(i, discovered)
    
    return discovered
    
print(dfs_recur(1))
```

- DFS 응용 (여행 일정 재구성)

```
from typing import List
import collections

class Solution:
    def findItinerary(self, tickets: List[List[int]]) -> List[str]:
        graph = collections.defaultdict(list)

        for a, b in sorted(tickets, reverse=True):
            graph[a].append(b)

        route = []
        def dfs(a):
            while graph[a]:
                dfs(graph[a].pop())
            route.append(a)

        dfs('JFK')
        return route[::-1]


graph = [["JFK", "SF0"], ["JFK", "ATL"], ["SF0", "ATL"], ["ATL", "JFK"], ["ATL", "SF0"]]

print(sorted(graph, reverse=True))

aa = []
ans = Solution()
aa=ans.findItinerary(graph)
print(aa)
```


