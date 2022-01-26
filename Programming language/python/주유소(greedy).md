#Greedy(그리디) 알고리즘 - 주유소

def gas_station(gas, cost):
    if sum(gas) < sum(cost):
        return -1
    
    start = 0
    fuel = 0
    for i in range(0, len(gas)):
        
        
        if gas[i]+fuel < cost[i]:
            start = i + 1
            fuel = 0
        
        else:
            fuel += gas[i]-cost[i]
            
    
    return start
    

gas = [1,2,3,4,5]
cost = [3,4,5,1,2]

res = gas_station(gas, cost)
