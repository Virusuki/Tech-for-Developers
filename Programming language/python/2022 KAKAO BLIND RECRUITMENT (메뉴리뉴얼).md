# 메뉴리뉴얼

문제 - https://programmers.co.kr/learn/courses/30/lessons/72411

```
import itertools
from collections import Counter

orders = ["ABCFG", "AC", "CDE", "ACDE", "BCFG", "ACDEH"]   # 각(6명) 손님들이 주문한 메뉴 구성 
course = [2,3,4]                                           # 후보 코스 개수

answer = []

for single_course in course:
    temp = []
    for order in orders:
        combi = itertools.combinations(order, single_course)   
            # combinations함수를 이용한 각 손님들이 주문한 메뉴 order에서 nCr=n(order) C r(single_course) 2가지 코스를 뽑았을때 메뉴
              
        temp += combi

    counter = Counter(temp)  # Counter 함수를 사용하여 조합에서 뽑은 코스개수에 따른 중복되는 개수
                             # 예) ('A', 'C'): 4, ('C', 'D'): 3, ,,,
    print(counter)
#    print(max(counter.values()))

    if len(counter) != 0 and max(counter.values()) != 1:
        answer += {''.join(ord) for ord in counter if counter[ord] == max(counter.values())}

print(sorted(answer))
```
