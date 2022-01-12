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
    
    for i in graph[v]:
        if i not in discovered:
            discovered=dfs_recur(i, discovered)
    
    return discovered
    
print(dfs_recur(1))
