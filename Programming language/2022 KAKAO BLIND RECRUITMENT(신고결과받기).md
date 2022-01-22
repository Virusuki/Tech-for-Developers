## 2022 KAKAO BLIND RECRUITMENT
### 신고 결과 받기

문제 - https://programmers.co.kr/learn/courses/30/lessons/92334

```
from collections import defaultdict 

def solution(id_list, report, k):
    answer = [0] * len(id_list)
    
    report = set(report)  # 문제의 핵심은 중복 값을 제거
    
    reporter_dict = defaultdict(set)            # 유저ID  -> 유저가 신고한 ID (딕셔너리)
    number_of_be_reported = defaultdict(int)    # 유저ID가 신고당한 횟수 (딕셔너리)
    
    suspend = []
    
    for r in report:
        do_report, be_reported = r.split()        
        
        reporter_dict[do_report].add(be_reported)     # 예) 'muzi': {'neo', 'frodo'}...
        number_of_be_reported[be_reported] += 1       # 예) 'muzi': 1, 'neo': 2, 'frodo': 2 (신고당한 횟수)
    
        if number_of_be_reported[be_reported] == k:   # 2번 신고당한 유저는 suspend 리스트에 append
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
```
