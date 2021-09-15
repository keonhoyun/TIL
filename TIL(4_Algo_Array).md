# :page_facing_up: TIL 배열



## :large_blue_circle: 버블정렬 O(n²) /  O(n²) 

### 개념

- 인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식
  - 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동한다.
  - 한 단계가 끝나면 가장 큰 원소가 마지막 자리로 정렬된다.
- 시간복잡도 == O(n²)

### 코드(버블정렬)

```python
def BubbleSort(a):
    # 길이가 4면 인덱스는 3까지이므로 len에 -1를 해준다.
    for i in range(len(a)-1, 0, -1):
        for j in range(0, i):
            # 버블 오름차순 정렬
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
            # 내침차순 정렬
            if a[j] < a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]                
```



## :candy: 카운팅정렬 O(n+k) / O(n+k) 

### 개념

- 항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 센느 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘

- 정수나 정수로 표현할 수 있는 자료에 대해서만 적용 가능
  - 각 항목의 발생 횟수를 기록하기 위해 정수 항목으로 인덱스 되는 카운트들의 배열을 사용하기 때문
- 카운트들을 위한 충분한 공간을 할당하려면 집합 내의 가장 큰 정수를 알아야함

- 시간복잡도 == O(n + k): n은 리스트 길이, k는 정수의 최대값

### 코드(카운팅  정렬)

```python
def Counting_Sort(A, B ,K):
    # 0 ~ k까지 인덱스를 담을 리스트 
    C = [0] * k + 1
    
    for i in range(0, len(A)):
        C[A[i]] += 1
        
    for i in range(1, len(C)):
        C[i] += C[i-1]
        
    for i in range(len(A)-1, -1, -1):
        B[C[A[i]]] = A[i]
        C[A[i]] -= 1
    
```



## :tangerine: 선택정렬 O(n²) /  O(n²)

### 개념

- 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식
- 최소값 찾기
- 맨 앞 값이랑 교환
- 맨 처음 위치 제외 다시 반복

### 코드

```python
def selectionSort(a):
    # 다음 요소와 비교해야 하므로 len(a) -1 해주기
    for i in range(0, len(a)-1):
        # 처음 값을 최소값이라 가정
        minidx = i
        # 다음 요소부터 배열 끝가지 탐색
        for j in range(i+1, len(a)):
            # 최소값보다 작은 값이 나오면
            # minidx 바꾸기
            if a[minidx] > a[j]:
                minidx = j
        a[i], a[mindix] = a[mindix], a[i]
```



## 순열

### 코드( 3! )

```python
for i1 in range(1, 4):
    for i2 in range(1, 4):
        if i2 != i1:
            for i3 in range(1, 4):
                if i3 != i1 and i3 != i2:
                    print(i1, i2, i3)              
```



## :flower_playing_cards: Baby Gin

```python
num = int(input()) # ex) 456789
C = [0] * 12 # 나중에 반복문 돌릴 때 인덱스 에러 안나기 위함

for i in range(6): # num의 길이
    C[num % 10] += 1
    num //= 1
   
i = 0
tri = run = 0
while i < 10:
    if C[i] >= 3: # triplete 조사 후 삭제
        C[i] -= 3
        tri += 1
        continue
    if C[i] >= 1 and C[i+1] >= 1 and C[i + 2] >= 1: # run 조사 후 삭제
        c[i] -= 1
        c[i + 1] -= 1
        c[i + 2] -= 1
        run += 1
        continue
    i += 1
if run + tri == 2:
    print("Baby Gin")
else:
    print("Lose")
```



## :taxi: 배열순회



### 행 우선

```python
# 행 우선 순회
for i in range(len(arr)):
    for j in range(len(arr)):
        arr[i][j]
```

### 열 우선

```python
# 열 우선 순회
for i in range(len(arr)):
    for j in range(len(arr)):
        arr[j][i]
        
# 또는
for j in range(len(arr)):
    for i in range(len(arr)):
        arr[i][j]
```

### 지그재그

```python
# 지그재그 순회
for i in range(len(arr)):
    for j in range(len(arr)):
        arr[i][j + (len(arr)-1 - 2*j) * (i % 2)]
        
```

### 델타를 이용한 탐색

```python
di = [0, -1, 0, 1] # 행(세로이동)
dj = [1, 0, -1, 0] # 열(가로이동) # 시계뱡항으로 우, 하, 좌, 상
change = 0 # 방향값 0으로 초기화

for i in range(len(arr)):
    for j in range(len(arr)):        
        ni, nj = i + di[change], j + dj[change] # 다음 좌표
        i, j = ni, nj
        change = (change + 1) % 4
```



## 전치행렬

```python
# 대각선 기준 뒤집기
for i in range(len(arr)):
    for j in range(len(arr)):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
            
#  zip 함수 쓰기
arr2 = list(zip(*arr))
```



## 비트연산자

### 부분집합 구하기

```python
arr = [3, 6, 5, 7, 1, 4]

n = len(arr)

for i in range(1 << n):
    for j in range(n+1):
        if i & (1<<j):
            print(arr[j], end = ", ")
        print()
```



### 순차검색

```python
# 정렬되어있지 않은 경우
def sequentialSearch(a, n, key):
    i = 0
    # i가 찾을 리스트의 길이보다 작거나, key값이랑 일치 하지 않으면
    # 다음 인덱스로
    while i < n and a[i] != key: 
        i += 1
    # i가 n보다 작은 상황이면 i 반환(key값이 같으면 위 조건 탈출이기 때문)
    if i < n:
        return i
    # 그 이외의 경우는 검색 실패!
    else:
        return -1
    
# 정렬되어 있는 경우
def sequentialSearch(a, n, key):
    i = 0
    # 배열의 길이보다 작거나, 키 값보다 작으면 다음 인덱스로
    while i < n and a[i] < key:
        i += 1
    # 키 값을 찾았으면 인덱스 반환
    if i < n and a[i] == key:
        return i
    # 정렬되어 있으므로 key값보다 크면 검색 실패
    else:
        return -1
    
```



### 이진검색

```python
def binarySearch(arr, key):
    # 시작값 0
    start = 0
    # 마지막 인덱스는 길이 -1 이므로
    end = len(arr) - 1
    # 시작값이 끝 값보다 작은 경우 계속 반복문 돌리기
    while start <= end:
        # 중간값은 시작값과 끝을 더하고 2로 나누기
        middle = (start + end) // 2
        # 찾으면 True
        if arr[middle] == key:
            return True
        # 중간값이 키 값보다 크면 작은 쪽으로 범위를 줄이기
        elif arr[middle] > key:
            end = middle - 1
        # 중간값이 키 값보다 작으면 큰 쪽으로 범위 줄이기
        else:
            start = middle + 1
    return False
```

```python
# 재귀 버전
def binarySearch(arr, low, high, key):
    # 검색 실패
    if low > high:
        return False
    else:
        middle = (low + high) // 2
        # 검색 성공
        if key == arr[midde]:
            return True
        # 중간값이 키 값보다 크면 작은 쪽으로 범위를 줄여서 재귀
        elif key < arr[middle]:
            return binarySearch(a, low, middle-1, key)
        # 중간값이 키 값보다 작으면 큰 쪽으로 범위를 줄여서 재귀
        elif key > arr[middle]:
            return binarySearch(a, middle+1, high, key)
    
```

