# 2020 KAKAO BLIND RECRUITMENT (문자열 압축)

문제 - https://programmers.co.kr/learn/courses/30/lessons/60057?language=python3

```
s = "abcabcdede"  # 2abcdede
#abab cdcd abab cdcd
result = []

if len(s) == 1:
    print(1)


for i in range(1, (len(s)//2)+1  ):
    b = ''
    cnt = 1
    tmp=s[:i]
    print(tmp)
    for j in range(i, len(s), i):
        if tmp == s[j:i+j]: 
            cnt += 1
        else:
            b = b + tmp
        tmp = s [j:j+i]
        cnt = 1
    if cnt != 1:
        b = b + str(cnt) + tmp
    else:
        b = b + tmp
    result.append(len(b))

print(min(result))
```
