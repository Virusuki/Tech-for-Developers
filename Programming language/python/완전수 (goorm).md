# 완전수 (goorm)

문제 - https://level.goorm.io/exam/43275/%EC%99%84%EC%A0%84%EC%88%98/quiz/1

```
A, B = map(int, input().split())

ans = []

for i in range(1, B+1):
    sum = 0
    for j in range(1, i):  # i=6,
        if i % j == 0:
            sum += j
            
    if sum == i:
        ans.append(i)
print(ans)
```
