## 2022 KAKAO BLIND RECRUITMENT
### 주차요금 계산

문제 - https://programmers.co.kr/learn/courses/30/lessons/92341

- 이 문제의 포인트는 주차번호 오름차순을 위한 람다를 이용한 sort_list.sort(key=lambda x: x[0]) 함수 부분과 
  math.ceil()함수를 사용한 반올림이다.



```
import math

def convert_to_time(date):                 # 해당 함수는 주차시간 예)05:34 에 대한 시간+분을 파싱하여 minute(분) 추출 함수
    h, m = map(int,date.split(':'))
#    print(h, m)
    return h*60 + m


def solution(fees, records):
    answer = []
    
    in_out_record = dict()
    
    for r in records:
        time, car_num, flag  = r.split()
        car_num = int(car_num)
        
        if car_num in in_out_record:
            in_out_record[car_num].append([convert_to_time(time), flag])
        else:
            in_out_record[car_num] = [[convert_to_time(time), flag]]
    
    sort_list = list(in_out_record.items())
    sort_list.sort(key=lambda x: x[0])
    
    for car_his in sort_list:
         m_time = 0
         for car_times in car_his[1]:
             if car_times[1] == 'IN':
                 m_time -= car_times[0]
             
             else:
                 m_time += car_times[0]
         
         if car_his[1][-1][1] == 'IN':
            m_time += convert_to_time('23:59')
            
         
         if fees[0] >= m_time:
             answer.append(fees[1])
         else:
             print(m_time)
             answer.append(fees[1]+ math.ceil((m_time-fees[0])/10) * 600)

    return answer

fees = [180, 5000, 10, 600]    # 180 default minute, 5000 fee | per 10 min -> 600 won fee
records = [
    "05:34 5961 IN", 
    "06:00 0000 IN", 
    "06:34 0000 OUT", 
    "07:59 5961 OUT", 
    "07:59 0148 IN", 
    "18:59 0000 IN", 
    "19:09 0148 OUT", 
    "22:59 5961 IN", 
    "23:00 5961 OUT"
    ]    

answer = solution(fees, records)
print(answer)
```
