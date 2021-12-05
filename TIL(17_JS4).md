# TIL_16

## AJAX

### AJAX

- Asynchronous JavaScript and XML(비동기식 javascript와 xml)
- 서버와 통신하기 위해 XMLHttpRequest 객체를 활용
- JSON, XML, HTML 그리고 일반 텍스트 형식 등을 포함한 다양한 포멧을 주고받을 수 있음

- 페이지 전체를 새로고침 하지 않고서도 수행되는 비동기성



```javascript
const request = new XMLHttpRequest()
const URL = 'https://~~~'

request.open('GET', URL)
request.send()

const todo = request.response
console.log(`data: ${todo}`)

# todo 데이터가 출력되지 않음
# 데이터 응답을 기다리지 않고 console.log()를 먼저 실행했기 때문
```



### 동기식

- 순차적, 직렬적 Task 수행
- 요청을 보낸 후 응답을 받아야만 다음 동작이 이루어짐



### 비동기식

- 병렬적 Task 수행
- 요청을 보낸 후 응답을 기다리지 않고 다음 동작 이루어짐



### Threads

- 프로그램 작업을 완료하기 위해 사용할 수 있는 단일 프로세스
- 각 스레드느 한 번에 하나의 작업만 수행할 수 있음
- JavaScript는 single threaded이다.
  - 이벤트를 처리하는 Call Stack이 하나이다.
  - 즉시 처리하지 못하는 이벤트를 다른 곳으로 보내서 처리(Web API)
  - 처리된 이벤트들은 대기실(Task queue)에 줄을 세워 놓음
  - Call Stack이 비면 담당자(Event Loop)가 대기 줄에서 가장 오래된 이벤트를 Call Stack으로 보냄

### 동시성 모델

- Event loop를 기반으로 하는 동시성 모델
  - Call Stack - 요청이 들어올 때마다 해당 요청을 순차적으로 처리
  - Web API - 브라우저 영역에서 제공하는 API
  - Task Queue - 비동기 처리된 callback 함수가 대기하는 Queue 형태의 구조
  - Event Loop - Call Stack이 비어 있는지 확인

