# :page_facing_up: TIL_Stack

## Stack

- 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조
- 선형구조를 가짐
- 후입선출(Lasg-In-First-Out)



### 연산

- 삽입: 저장소에 자료를 저장함 보통 push로 일컫는다.
  - append 활용
- 삭제: 저장소에서 자료를 꺼낸다. 보통 pop이라고 일컫는다.
  - pop 활용

```python
def push(item):
    stack.append(item)
```

```python
def Pop():
    if stack:
        stack.pop() or stack.pop(-1)
```



### 재귀호출

``` python
def fibo(n):
    if n < 2:
        return n
    else:
        retrn fibo(n-1) + fibo(n-2)
```

### Memoization

- 이전에 계산한 값을 메모리에 저장, 다시 계산하지 않도록 함.
  - 실행속도를 빠르게 개선 可能
- meorization과 혼동할 수 있지만, 엄연히 다른 단어!

```python
def fibo_memo(n):
    global memo
    if n >= 2 and len(memo) <= n:
        memo.append(fibo_memo(n-1) + fibo_memo(n-2))
    return meomo[n]
        
memo = [0, 1]
```



### 동적계획

- 입력 크기가 작은 부분 문제들을 모두 해결한 후 그 해들을 이용하여 큰 크기의 부분 문제 해결하는 방식

```python
def fibo_dp(n):
    f = [0, 1]
    
    for i in range(2, n + 1):
        f.append(f[i-1] + f[i-2])
        
    return f[n]
```



## DFS

### 깊이 우선 탐색

- 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 반복하는 순회방법
- 후입선출 구조의 스택  사용

```python
adj = [[0] * (V + 1) for _ in range(V+1)] # 주어진 간선 정보로 인접 행렬 채워넣기
visited = [0] * [v + 1]
stack = [start]
def DFS(v):    
    visited[start] = 1 # 시작점 방문
    while stack:
        t = stack.pop()
        for i in range(1, V+1):
            if adj[t][i] == 1 and visited[i] == 0:
                visitied[i] = 1
                stack.append(i)	
```

```python
def dfs(s, V): # s 시작정점, V 마지막 정점(1번부터 시작하는 정점의 개수)
    stack = [] # 지나온 정점을 저장(경로)
    visited = [0] * (V+1) #  정점의 방문여부를 표시
    # 시작정점은 무조건 방문 (별도로 처리) 이후에는 가능한 정점만 방문
    i = s # 시작정점을 방문 (방문중인 정점의 번호 i)
    visited[i] = 1  # i 정점에 방문했음을 표시
    while i: # 유효한 정점은 0 < i, 정점에 방문한 생태면
        for w in range(1, V+1): # 인접하고 방문안한 정점 w 찾기기
            if adj[i][w] == 1 and visited[w] == 0:
                stack.append(i) # 현재 정점을 경로로 저장
                i = w # w에 방문 (현재 방문한 정점을 i)
                visited[i] = 1
                break # 다른 w 찾기 중단(for문 탈출)
        else: # 다음 방문할 정점이 없는 경우
            # 지나온 경로중 가장 가까운 정점을 꺼내 i로 지정
            if stack: # 스택이 비어있지 않은경우
                i = stack.pop()
            else: # 경로가 남아있지 않으므로 종료
                i = 0 # 없는 정점을 방문정점 번호로 설정..
    return # def dfs(s, V):


#          A  B  C  D  E  F  G
adj = [[0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 1, 1, 0, 0, 0, 0], # A
       [0, 1, 0, 0, 1, 1, 0, 0], # B
       [0, 1, 0, 0, 0, 1, 0, 0], # C
       [0, 0, 1, 0, 0, 0, 1, 0], # D
       [0, 0, 1, 1, 0, 0, 1, 0], # E
       [0, 0, 0, 0, 1, 1, 0, 1], # F
       [0, 0, 0, 0, 0, 0, 1, 0]] # G
node = ['', 'A','B','C','D','E','F','G']

dfs(1, 7)
```



## 계산기

### 계산기

```python
for tc in range(1,11):
    N = int(input())
    text = input()
    # 후위계산식을 담을 빈 문자열 생성
    ans = ''
    # 연산자를 담을 빈 스택 생성
    stack = []
    for i in text:
        # 곱하기 연산자가 나오면 스택에 쌓기
        if i == '*':
            stack.append(i)
        # 더하기 연산자가 나오면 남아 있는 스택의 값을 pop() 하기
        elif i == '+':
            while stack:
                ans += stack.pop()
            # 다시 자기를 스택에 쌓기
            stack.append(i)
        # 연산자가 나오지 않으면 후위계산식에 숫자 담기
        else:
            ans += i
    # 스택이 남아 있으면 모조리 후위계산식에 넣기
    while stack:
        ans += stack.pop()

    # 후위계산식을 계산할 빈 리스트 생성
    result = []
    # 후위계산식을 돌며
    for i in ans:
        # 곱하기 연산자가 나오면
        # 앞의 두 숫자를 불러와서 곱하기
        if i == '*':
            emp2 = result.pop()
            emp1 = result.pop()
            emp3 = emp1 * emp2
            # 결과값 리스트에 다시 넣기
            result.append(emp3)

        elif i == '+':
            # 더하기 연산자가 나오면 앞의 두 숫자를 더해서 다시 담기
            emp2 = result.pop()
            emp1 = result.pop()
            emp3 = emp1 + emp2
            result.append(emp3)

        # 숫자가 나오면 int 형태로 바꿔서 그냥 담기
        else:
            result.append(int(i))

    print("#{} {}".format(tc, result[0]))
```

```python
for tc in range(1,11):
    N = int(input())
    strings = str(input())
    # 빈 스택 만들기
    stack = []
    # 후위계산식을 만들 빈 리스트 생성
    numbers = []
    icp = {'*': 2, '+': 1, '(': 3}

    isp = {'*': 2, '+': 1, '(': 0}

    for string in strings:
        # 숫자가 나오는 경우 리스트에 담기
        if string.isdigit():
            numbers.append(string)

        # 연산자가 나온다면
        else:
            # 스택이 비어있다면 무조건 담기
            if not stack:
                stack.append(string)


            # 비어있지 않은 경우
            elif stack:
                # 닫는 괄호가 나오면 여는 괄호가 나올 때까지 넘버에 담기
                if string == ')':
                   while stack[-1] != '(':
                       numbers.append(stack.pop())
                    # 여는 괄호 제거
                   stack.pop()

                # 우선순위를 비교하기
                elif icp[string] > isp[stack[-1]]:
                    # 우선순위가 높은 경우 스택에 담기
                    stack.append(string)

                else:
                    #icp가 isp 보다 작으면 계속 pop해서 리스트에 담기
                    while icp[string] <= isp[stack[-1]]:
                        numbers.append(stack.pop())
                    # 마지막 스택 제거
                    stack.append(string)

    # 계산 결과를 담을 빈 리스트 선언
    ans = []
    # 리스트를 돌며 숫자면 담기
    for number in numbers:
        if number.isdigit():
            ans.append(number)

        else:
            # 연산자가 나오면 숫자 두 개 가져오기
            num2 = int(ans.pop())
            num1 = int(ans.pop())

            if number == "+":
                result = num1 + num2

            elif number == "*":
                result = num1 * num2
            # 계산결과 다시 담기
            ans.append(str(result))

    print('#{} {}'.format(tc, ans[0]))
```



## Queue

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
  - 뒤에서는 삽입만, 앞에서는 삭제만!
- 선입선출구조(FIFO)
  - 삽입한 순서대로 원소 저장, 가장 먼저 삽입된 원소는 가장 먼저 삭제



### 선형큐

- 1차원 배열을 이용한 큐
  - 큐의 그기 = 배열의 크기
  - front 저장된 첫 번째 원소의 인덱스
  - rear 저장된 마지막 원소의 인덱스
- 상태 표현
  - 초기 상태 : front = rear = -1
  - 공백 상태 : front = rear
  - 포화상태 : rear = n-1 (n: 배열의 크기, n-1: 배열의 마지막 인덱스)

### 삽입_enQueue

```python
# 선형 큐
def enQueue(item):
    global rear
    if isFull():
        print("Queue_Full")
    else:
        rear += 1
        Q[rear] = item
# 원형 큐
def enQueue(item):
    global rear
    global rear
    if isFull():
        print("Queue_Full")
    else:
        rear = (rear + 1) % len(cQ)
        Q[rear] = item
    
```

### 삭제_deQueue

```python
# 선형 큐
deQueue():
    if isEmpty():
        print("Queue_Empty")
    else:
        front += 1
        return Q.pop(front)
    
# 원형 큐
deQueue():
    if isEmpty():
        print("Queue_Empty")
    else:
        front = (front + 1) % len(cQ)
        return Q.pop(front)
```



### 큐 연습문제

```python
# 치즈 녹일 함수 만들기
def oven(pizza, N):
    queue = []
    # N 길이 만큼 큐에 담기
    for _ in range(N):
        queue.append(pizza.pop(0))
    # 큐의 길이가 1보다 크면 계속 반복문 돌리기
    while len(queue) > 1:
        # 큐에서 하나꺼내서 녹이기
        cheeze = queue.pop(0)
        # // 2 하기
        cheeze[1] //= 2
        # 아직 다 안녹았다면 끝으로 보내기
        if cheeze[1] > 1:
            queue.append(cheeze)
        # 피자가 남아있으면 큐에 넣기
        elif pizza:
            queue.append(pizza.pop(0))
    # 큐에 하나밖에 안남았다면(마지막 피자라면)
    return queue[0][0]

T = int(input())
for tc in range(1, T + 1):
    N, M = map(int, input().split())
    # 피자 배열 받아오기
    pizza = list(map(int, input().split()))
    # 피자와 인덱스 결합하기
    pizza_idx = []
    for idx, cheeze in enumerate(pizza):
        pizza_idx.append([idx + 1, cheeze])

    print('#{} {}'.format(tc, oven(pizza_idx, N)))
```



## BFS

### 너비우선탐색

- 인접한 정점들을 먼저 모두 차례로 방문
- 선입선출 형태의 큐를 활용

```python
def BFS(G, V):
    visited = [0] * (n+1)
    queue = []
    queue.append(v)
    while queue:
        t = queue.pop(0)
        if not visited[t]:
            visited[t] = 1
        for i in G[t]:
            if not visited[i]:
                queue.append[i]
```



### BFS 연습문제

```python
# Bfs 함수 만들기
def Bfs(S, End):
    # 큐에 시작점 담기
    queue = [S]
    # 큐가 있으면 반복문 계속 돌리기
    while queue:
        # 시작점 꺼내오기
        t = queue.pop(0)
        # t가 끝점에 오면
        if t == End:
            # 방문점에 있는 값 출력
            return visited[t]
        # 그게 아니면 인접리스트에 있는 값 불러오기
        for i in adj[t]:
            # 만약 방문 안 한 곳이면
            if visited[i] == 0:
                # 큐에 넣기
                queue.append(i)
            # 앞 값 + 1 (거쳐간 횟수 구하기 위함)
            visited[i] = visited[t] + 1
    return 0

T = int(input())
for tc in range(1, T + 1):
    # V, E 받아오기
    V, E = map(int, input().split())
    # 인접리스트 생성
    adj = [[] for _ in range(V + 1)]
    # 방문한 곳 체크할 리스트 생성
    visited = [0] * (V + 1)
    for _ in range(E):
        # 인접한 곳 표시할 a, b 받아오기
        a, b = map(int, input().split())
        # 인접리스트에 넣기 ----- [[2], [1]] - 1번은 2번과 인접 / 2번은 1번과 인접
        adj[a].append(b)
        adj[b].append(a)
    # 시작점과 끝 점 받아오기
    Start, End = map(int, input().split())

    print('#{} {}'.format(tc, Bfs(Start, End)))
```

