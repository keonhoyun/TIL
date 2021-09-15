# :page_facing_up: TIL String

## ASCII 코드

- 네트워크가 발전하면서 서로간에 정보를 주고 받을 때 정보를 달리 해석하는 문제 발생
- 표준안 개발의 필요성 대두
- ASCII 표준 재정(American Standard Code for Information Interchange)
- 7bit 인코딩으로 128문자 표현



## 유니코드

- 미국 뿐 아니라 각 나라에서도 컴퓨터가 발전하며 자국의 문자를 표현하기 위한 코드체계 발명

- 다국어 처리를 위해 표준 마련

- 유니코드 인코딩

  - UTF-8(web)

    -- Min: 8bit, Max: 32bit

  - UTF-16(window, java)

    -- Min: 16bit, Max: 32bit

  - UTF-32(unix)

    -- Min: 32bit, Max: 32bit



## 패턴 매칭

### 고지식한 패턴 매칭 (  O(MN))  )

```python
patten = str(input())
text = str(input())
M = len(patten)
N = len(text)

def BruteForce(patten, text):
    # 시작 인덱스 초기화
    i = 0
    j = 0
   	while j < M and i < N: 
        if text[i] != patten[j]:
            # 다르면 초기화 (text는 다음 순서)
            # 패턴은 0부터 시작하도록
            i = i - j
            j = -1
        # 다음 인덱스로
        i = i + 1
        j = j + 1
    if j == M: # 검색성공
        return True
    else:
        return -1
```



### KMP 알고리즘 (  O(M + N)  )

```python
# next: 0 0 0 0 0 0 0 0 0 
# text: a b c d a b c e f
# chK :   a b c d a
# chK :     a b c d a
# chK :       a b c d a
# chK :         a b c d a
# next: 0 0 0 0 1 2 3 0 

next = [0] * M (M =문자열 길이)
cnt = 0 # 일치한 개수
i = 1 # 1번 인덱스부터 비교(=패턴 찾기)
while i < M:
    # 패턴이 일치하면 cnt += 1
    if p[i] == p[cnt]:
        cnt += 1
        next[i] = cnt
        i += 1
    else:
        if cnt != 0:
            # 앞 단어와 일치할 수 있으므로 바로 앞 단어와 비교
            # e자리에 d와 불일치이므로 앞 단어인 c와 비교
            cnt = next[cnt - 1]            
        else:
            next[i] = 0
            i += 1
```









