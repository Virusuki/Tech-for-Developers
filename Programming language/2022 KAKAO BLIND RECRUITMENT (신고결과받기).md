## 2022 KAKAO BLIND RECRUITMENT
### 신고 결과 받기

문제 - https://programmers.co.kr/learn/courses/30/lessons/92334

이 문제의 접근 방식은 dictionary(딕셔너리)와 defaultdict를 사용
defaultdict는 value의 타입만 지정해준다면 key 값에 매핑되는 value를 디폴트 값으로 지정되어 있다.


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
    
    for sus in suspend:                               # 유저가 신고했던 ID 중 2번이상 신고 당한 유저에 대해 반복
        for i in range(len(id_list)):                 
            #if sus in reporter_dict[id_list[i]]:
            if sus in reporter_dict[id_list[i]]:      # 유저ID  -> 유저가 신고한 ID (딕셔너리) 중 2번 이상 신고당한 유저가 있다면, 
                answer[i] += 1                        # id_list 순서의 각 유저 별(신고한유저) 카운트

    return answer

id_list = ["muzi", "frodo", "apeach", "neo"]

report = ["muzi frodo","apeach frodo","frodo neo","muzi neo","apeach muzi"]    

ans = solution(id_list, report, 2)
print(ans)
```
