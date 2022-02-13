# 깊이/너비 우선 탐색(DFS/BFS) - 단어 변환 (프로그래머스)


문제 - https://programmers.co.kr/learn/courses/30/lessons/43163

from collections import deque 

def solution(begin, target, words):
    v = [ 0 for i in range(len(words))]
    answer= 0 
    q = deque()
    q.append((begin, 0))
    
    while q:
        
        q_word, cnt = q.popleft()
        
        if q_word == target:
            answer = cnt
            break
        
        for i in range(len(words)):
            tmp_cnt=0
            if not v[i]:                
                for j in range(len(q_word)):
                    if q_word[j] != words[i][j]:
                        tmp_cnt += 1
                if tmp_cnt == 1:
                    q.append((words[i], cnt+1))
                    v[i] = 1
    return answer
                    

words = ["hot", "dot", "dog", "lot", "log", "cog"]    
begin = "hit"    
target = "cog"    

res = solution(begin, target, words)

print(res)
