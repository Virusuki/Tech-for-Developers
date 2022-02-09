# 2019 KAKAO BLIND RECRUITMENT (오픈채팅방)

문제 - https://programmers.co.kr/learn/courses/30/lessons/42888

```
Id_DB = {}

Record = ["Enter uid1234 Muzi", "Enter uid4567 Prodo","Leave uid1234","Enter uid1234 Prodo","Change uid4567 Ryan"]

actions = []
answer = [] 
 
for rcd in Record:
    info = rcd.split()
    act, uid = info[0], info[1]
    
    if act in ["Enter", "Change"]:
        nic = info[2]
        Id_DB[uid] = nic
    actions.append((act, uid))

for action in actions:
    behavior, id = action[0], action[1]
    
    if behavior == "Enter":
        answer.append(f'{Id_DB[id]} Enter.')
    
    elif behavior == "Leave":
        answer.append(f'{Id_DB[id]} Leave.')

print(answer)
```
