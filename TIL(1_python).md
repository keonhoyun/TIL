# :memo: TIL 0723

MAP은 리스트 각 요소에 설정하기

```python
a = [85, 87, 66]
map(chr, a) ->  # a 리스트 각 요소를 chr함수 적용
```

list의 각요소는 굳이 len으로 돌려서 할필요가 없었다..... ㅠㅠ



## 관통프로젝트

- $ 은 프롬포트(promport) 이게 있어야 명령어 가능
  - $ $ 이렇게 적으면 (X) $ git ~~~ (O)

- / : Root directory : 최상단 
- ~ : Home directory 사용자(계정)에게 할당된 폴더
- . : 현재 위치한 폴더를 지칭
- .. : 상위 폴더를 지칭
- Tab : 파일/폴더 이름 자동완성
  - cli 치고 TAB --> cli로 시작 자동완성
- ctrl + C : 실행중인 프로세스 취소 (cancel)
- ctrl + L  : 터미널 창 정리하기
- 방향키(up), 방향키(down) : 명령어 기록 탐색



###  명령어

- rm -r -> 지정한 폴더 및 파일 삭제
- rm -rf -> 강제 삭제



### :warning: WARING

- Home 폴더에서 초기화 하지 않기!
- git init 한 폴더에서는 git init 하지 않기!



## 이모지

:smile:

: 하고 검색하기

:page_with_curl:



technical writing

## 코딩 시 

키보드로 먼저 손이 가지 말고 말로 풀어보자 (주석으로)

## print return

- print : 디버깅 용 / output과는 무관
- return: 함수에서 return을 만나면 종료 = else값이 필요없음



## key value

딕셔너리

for data in user_data:

print(data)는 키값!!



## 빈문자열

bool('')  -> False



## get

dict 에서 key 로 value찾기

my.dict['key'] -> key가 없으면 에러

my.dict.get('key') -> key가 없으면 None을 발생



## open

