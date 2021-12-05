[TOC]

# 1. 완전검색 / 그리디

**완전검색 => 순열, 조합, 집합, 조합적 문제들과 연관 즉 조합적 문제에 대한 brute force 방법**

## 1) 조합적 문제

### (1) 순열(Permutation)



- {1, 2, 3} 을 포함하는 모든 순열을 생성하는 함수

  ```python
  for i1 in range(1, 4):
      for i2 in range(1, 4):
          if i2 != i1:
              for i3 in range(1, 4):
                  if i3 != i1 and i3 != i2:
                      print(i1, i2, i3)
  ```

- **nPn**

  ```python
  # 3 개 숫자 중 3개 뽑기
  # p : 순열을 저장하는 배열
  # arr[i] : 순열을 만드는데 사용할 숫자배열
  # n 원소의 개수, i 는 선택된 원소의 수, k 자리를 정할 인덱스
  
  def permutation(n, k):
      if k == n:
          print(p)
      else:
          if i in range(n):    # 모든 원소에 대해
              if not used[i]:  # 아직 사용된 적 없으면
                  p[k] = arr[i] # 순열에 사용
                  used[i] = True  # 사용됨으로 표시 (True = 1, False = 0 으로 해도 됨)
                  permutation(n, k+1) # 다음칸 채우기
                  used[i] = False  # 현재 칸 이제 쓸일 없어, 다음 칸에서 쓸 수 있게 풀어주기
                  
  p = [0] * 3
  arr = [1, 2, 3]  # 이게 정렬되야 사전 순서대로 나옴
  u = [0] * 3              
  ```

- **nPr**

  ```python
  # 5개 중 3개 뽑기
  p = [0] * 3
  arr = [1, 2, 3, 4, 5]  # 이게 정렬되야 사전 순서대로 나옴
  u = [0] * 5
  f(3, 5, 0)
  
  def permutation(n, m, k):
      if k == n:
          print(p)
      else:
          if i in range(m):    # 주어진 숫자의 개수만큼
              if not used[i]:  # 아직 사용된 적 없으면
                  p[k] = arr[i] # 순열에 사용
                  used[i] = True  # 사용됨으로 표시 (True = 1, False = 0 으로 해도 됨)
                  permutation(n, m, k+1) # 다음칸 채우기
                  used[i] = False
  ```

  

- **재귀 호출**을 통한 순열생성

  ```python
  # n 원소의 개수, i 는 선택된 원소의 수, k 자리를 정할 인덱스
  
  def permutation(n, k):
      if k == n:
          print(p)
          return
      else:
          for i in range(k, n):
              p[k], p[i] = p[i], p[k]
              permutation(n, k+1)
              p[k], p[i] = p[i], p[k]
              
  p = [1, 2, 3]# 데이터가 저장된 배열
  permuation(3, 0)
  ```

  

- 첫 번째 뽑는 값 고정시키기

- ```python
  def permutation(n, k):
      if k == n:
          print(p)
      else:
          if i in range(n):    # 모든 원소에 대해
              if not used[i]:  # 아직 사용된 적 없으면
                  p[k] = arr[i] # 순열에 사용
                  used[i] = True  # 사용됨으로 표시 (True = 1, False = 0 으로 해도 됨)
                  permutation(n, k+1) # 다음칸 채우기
                  used[i] = False  # 현재 칸 이제 쓸일 없어, 다음 칸에서 쓸 수 있게 풀어주기
                  
  p = [0] * 5
  arr = [1, 2, 3, 4, 5]  # 이게 정렬되야 사전 순서대로 나옴.
  u = [0] * 5
  
  # 첫번째는 항상 1로 두려면?
  p [0] = arr[0]
  u[0] = 1  # 첫번째는 1로 고정하기 위함
  f(5, 5, 1)
  
  # 첫번째, 두번째는 1, 2로 채우고 그 다음부터 채우려면?
  p [0] = arr[0]
  p[1] = arr[1]
  u[0] = 1  # 첫번째는 1로 고정하기 위함
  u[1] = 1
  f(5, 5, 2)
  ```

  
  
- 순열 라이브러리 활용하기

  ```python
  from itertools import permutations
  
  print(permutations([1, 2, 3]))
  
  for case in permutations([1, 2, 3]):
  	print(case) # 튜플 형태로 나옴
  ```

  

### (2) 부분집합

- 집합에 포함된 원소들을 선택하는 것

- N개의 원소를 포함한 집합

  - 모든 부분집합(power set)의 개수는 2 ** n개

- 단순하게 모든 부분 집합 생성하는 방법

  ```python
  # 4개 원소를 포함한 집합에 대한 power set 구하기
  for i1 in range(2):
      bit[0] = i1
      for i2 in range(2):
          bit[1] = i2
          for i3 in range(2):
              bit[2] = i3
              for i4 in range(2):
                  bit[3] = i4
                  print(bit)
  ```

  

- 바이너리 카운팅을 통한 사전적 순서

  - {A,       B,   C,     D}

    bit0,     1,    2,     3    # 0번째 비트는 A의 포함 여부를 알려줌

    0/1     0/1  0/1   0/1

  ```python
  arr = [3, 6, 7, 1, 5, 4]
  n = len(arr)
  
  for i in range(1 << n):  # 2 **n 부분집합의 개수
      for j in range(n):   # j번째 비트를 검사하기
          if i & (1 << j):  # j번 비트가 1이면 j번째 원소를 출력
              print(arr[j])
  ```

  

  ```python
  # 재귀로 만들어보기
  # 0번 원소가 포함되거나 포함되지 않거나
  # 각각의 상황에서 다음 원소가 포함되거나 포함되지 않거나
  
  ```

  

### (3) 조합

- 재귀 호출을 이용한 조합 생성 알고리즘

  ```python
  arr = [] # n개의 원소를 가지고 있는 배열
  tr = [] # r개의 크기의 배열, 조합이 임시 저장 될 배열
  
  def comb(n, r):
      if r == 0:
          print(tr)
      elif n < r:
          return
      else:
          tr[r-1] = arr[n-1]
          comb(n-1, r-1)
          comb(n-1, r)
  ```



- n개에서 r개 고르는 조합 

  - **반복문** : i < j < k 라고 하면 (크기가 정해져있고, 고를 애가 많지 않을 때,)

  ```python
  # i는 적어도 왼쪽에 2개는 있어야 (j, k 몫)
  for i in range(8):  # j, k로 선택 될 원소를 남김  #(10-3-0) # 아직 0개 선택됐어.  
      for j in range(i+1, 9):					   #(10-3+1) #(n-r+k) 여기까지 고를 수 있어.
          for k in range(j + 1 , 10):			   #(10-3+2)
              # 여기서 나오는 값에 대해서 실시
              # f(a[i], a[j], a[k])
              print(i, j, k)
  ```

  

  - **재귀** : 원소 고를 시작구간(S), 이전까지 고른 원소의 개수(k), 전체 주어진 크기(n), 몇 개 고를 지(r)

  ```python
  # n개에서 r개를 고르는 조합, s 선택할 수 있는 구간의 시작, k 고른 개수
  def nCr(n, r, s, k):
      if k == r:
          print(*comb)
         else:
          for i in range(s, n-r+k+1): # n-r+k 선택할 수 있는 구간의 끝
              comb[k] = i
              nCr(n, r, i+1, k+1)
  
  N = 10
  R = 3
  comb = [0] * R
  nCr(N, R, 0, 0)
  ```

  

# 2.  분할정복 & 백트래킹

:star: 삼성 시험에서 아주 좋아하는 부분

## 1) 정렬

### (1) **병합정렬**(Merge Sort)

- 자료를 최소 단위의 문제까지 나눈 뒤에 차례대로 정렬해서 최종 결과를 얻어냄 

- O(nlogn)

  

- 분할과정 (인덱스로 진행하는 방법도 생각해보기. 지금 여기는 아예 리스트를 새로 생성.)

```python
def merge_sort(arr):
    # 만약 두 부분으로 나눌 수 없다면, 과정없이 arr을 그대로 반환
    if len(arr) == 1:
        return arr
    # 전체를 두 부분으로 나누는 부분
    mid = len(arr)//2
    left = arr[:mid]
    right = arr[mid:]
    # 나뉜 두 부분을 각각 merge_sort()를 실행
    left = merge_sort(left)
    right = merge_sort(right)
    # 각각에 대한 merge_sort()의 결과를 병합
    # 병합(merge) : 두 배열에서 작은 순서대로 요소를 가져와서 새로운 배열 만들기
    # 병합한 배열 반환
    return merge(left,right)

```



- 병합과정

```python
def merge(left,right):
    # arr1과 arr2를 병합한 배열을 반환
    result = []
    #병합하기
    i = j = 0
    # 복사할 배열 요소가 남아있으면 계속 반복
    left_len = len(left)
    right_len = len(right)
    while i < left_len or j < right_len:
        # 1. left와 right에 모두 복사할 요소가 남아있는경우
        # 2. left에만 남아있는 경우
        # 3. right에만 남아있는경우
        if i < left_len and j < right_len:  # 1번
            if left[i] < right[j]:
                result.append(left[i])
                i += 1
            else:
                result.append(right[j])
                j += 1
        elif i < left_len:  # 왼쪽 요소만 남음..
            result.append(left[i])
            i += 1
        elif j < right_len:  # 오른쪽 요소만 남음
            result.append(right[j])
            j += 1

    return result
```

=> 저장할 자리를 새로 만들고 있어서 메모리 낭비가 심함





### (2) **퀵정렬(Quick sort)**

- 주어진 배열을 두 개로 배열하고 각각을 정렬
- 병합 정렬은 그냥 두 부분으로 나누지만 퀵 정렬은 기준 아이템을 중심으로 작은건 왼편, 큰건 오른편
- 퀵정렬은 병합과정이 필요 없음
- https://medium.com/pocs/locality%EC%9D%98-%EA%B4%80%EC%A0%90%EC%97%90%EC%84%9C-quick-sort%EA%B0%80-merge-sort%EB%B3%B4%EB%8B%A4-%EB%B9%A0%EB%A5%B8-%EC%9D%B4%EC%9C%A0-824798181693

```python
def quicksort(A, l, r): # A는 정렬 대상, l부터 r까지 정렬해야함
    if l < r:
        s = partition(A, l, r)  # 중간 경계가 s, s는 두고, s보다 작은곳, s보다 큰 곳을 정렬
        quicksort(A, l, s - 1)
        quicksort(A, s + 1, r)
        
        
arr = [3, 2, 4, 6, 9, 1, 8, 7, 5]
quicksort(arr, 0, len(arr)-1)
print(arr)
```



- Hoare-Partition 알고리즘

```python
def partition(A, l, r):
    p = A[l]  # p: 피봇값 => 맨 왼쪽을 기준으로 해보자 (어떤걸 피봇값으로 정하는지에 따라서도 코드가 달라짐)
    i = l 
    j = r
    while i <= j: # 역전되기 전까지
        while i <= j and A[i] <= p: # i는 피봇보다 큰 애를 찾아서 오른쪽으로 이동
            i += 1
        while i <= j and A[i] >= p: # j는 피봇보다 작은 애를 찾아서 왼쪽으로 이동
            j -=1
        if i < j :  # 찾아서 멈췄는데 아직 교차하지 않은 상태이라면
            A[i], A[j] = A[j], A[i]  # 두개를 바꿔
             
    # 역전되었다면, j의 왼쪽에는 피봇보다 작은값, i의 오른쪽에는 피봇보다 큰 값만 모여있음.
    A[l], A[j] = A[j], A[l] # 피봇을 j와 교환
    return j
```



- Lomuto partition 알고리즘

```python
def lomuto_p(A, l, r):  # l는 구간의 시작
    pivot = A[r]  # 맨 오른쪽을 피봇으로 두자
    i = l - 1 # i는 경계구역  # 구간의 하나 전 인덱스

    for j in range(l,r):
        if A[j] <= pivot:  # 주어진 숫자가 중복 된 값이 있는 지에 대한 여부와 부등호 연관
            i += 1  # 여기서 i 는 pivot 기준으로 작은 값들의 가장 마지막 인덱스
            A[i], A[j] = A[j], A[i] # i는 작은 값들의 경계, i + 1은 큰 값 시작 인덱스

    A[i+1], A[r] = A[r], A[i+1]
    return i + 1
```





## 2) 트리

### (1) 힙(heap)

- **삽입 **
  - 완전 이진트리 : 마지막 정점 + 1, 마지막에 삽입
  - 최대힙 : 부모 노드(last//2) 키값과 비교하고 자식이 더 크면 바꾸기.
    - 부모가 더 크거나, 부모가 없으면 중단
    - 부모가 있고, 부모의 키값이 더 작으면, 교환
    - 부모를 새로운 자식으로 해서 반복

```python
def enq(n):
    global last
    last += 1
    tree[last] = n
    c = last
    p = c // 2
    while p >= 1 and tree[p] < tree[c]:
        tree[p], tree[c] = tree[c], tree[p]
        c = p
   		p = c // 2
    


 
tree = [0] * 101  # 최대 100번 노드까지  최대힙
last = 0          # 마지막 노드 번호
a = [7, 2, 3, 9, 5]
for x in a:
    enq(x)

```



- **삭제**
  - 루트 노드의 원소만 삭제 가능
  - 마지막 노드 삭제하고 싶으면,
    - 르트 원소 따로 빼두고
    - 마지막 원소를 루트 원소에 넣고, last 인덱스 값을 -1
    - 왼쪽 자식, 오른쪽 자식과 비교하면서, 두개 중에 큰 애를 부모 자리에 올리고, 얘를 자식 자리로 옮기기

```python
def deq():
    global last
    tmp = tree[1]
    tree[1] = tree[last] # 복사
    last -=1
    
    p = 1
    c1 = 2 * p
    c2 = 2 * p + 1
    
    while c1 <= last: # 자식이 하나라도 있으면
        if c2 <= last: # 자식이 둘이면
            if tree[c1] >= tree[c2] and tree[c1] > tree[p]:
                tree[c1], tree[p] = tree[p], tree[c1]
                p = c1
            elif tree[c1] < tree[c2] and tree[c2] > tree[p]:
                tree[c2], tree[p] = tree[p], tree[c2]
                p = c2
            c1 = p * 2
            c2 = P * 2 + 1
        
        else:		# 왼쪽 자식만 있는 경우
           if tree[c1] > tree[p]:        
        		tree[c1], tree[p] = tree[p], tree[c1]
                break
```





# 3. 그래프 & 백트래킹

## 1) 그래프 기본

> 인접 행렬

```python
'''
마지막 정점 번호, 간선 수
6 8
0 1 0 2 0 5 0 6 4 3 5 3 5 4 6 4
'''

V, E = map(int, input().split())
edge = list(map(int, input().split()))
adjM = [[0] * (V + 1) for _ in range(V + 1)]
for i in range(E):
    n1, n2 = edge[2*i], edge[2* i + 1]
    adjM[n1][n2] = 1
    adjM[n2][n1] = 1  # 무향 그래프인 경우
    
```

정점이 많으면 인접 행렬은 낭비.



> 인접 리스트

- 각 정점에 대한 인접 정점들을 순차적으로 표현

```python
'''
마지막 정점 번호, 간선 수
6 8
0 1 0 2 0 5 0 6 4 3 5 3 5 4 6 4
'''

V, E = map(int, input().split())
edge = list(map(int, input().split()))
    
# adj[출발지][도착지]
adjL= [[] for _ in range(V + 1)]
for i in range(E):
    n1, n2 = edge[2*i], edge[2* i + 1]
    adjL[n1].append(n2)  # 크기 순이 아니라, 입력된 순으로 저장됨
    adjL[n2].append(n1)  # 무향그래프인 경우
```

