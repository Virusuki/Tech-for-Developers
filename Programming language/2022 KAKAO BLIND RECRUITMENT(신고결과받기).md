# 신고 결과 받기

from collections import defaultdict 

def solution(id_list, report, k):
    answer = [0] * len(id_list)
    
    print(report)
    report = set(report)
    print(report)
    
    reporter_dict = defaultdict(set)
    number_of_be_reported = defaultdict(int)
    
    suspend = []
    
    for r in report:
        do_report, be_reported = r.split()
        
        reporter_dict[do_report].add(be_reported)
        number_of_be_reported[be_reported] += 1
    
        if number_of_be_reported[be_reported] == k:
            suspend.append(be_reported)    
    
    for sus in suspend:
        for i in range(len(id_list)):
            #if sus in reporter_dict[id_list[i]]:
            if sus in reporter_dict[id_list[i]]:
                answer[i] += 1              

    return answer

id_list = ["muzi", "frodo", "apeach", "neo"]

report = ["muzi frodo","apeach frodo","frodo neo","muzi neo","apeach muzi"]    

ans = solution(id_list, report, 2)
print(ans)
