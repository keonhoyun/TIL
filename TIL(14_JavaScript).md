# TIL_JS

## JavaScript 기초

### 브라우저

- 웹 서버에서 이동하며 클라이언트와 서버 간 양방향으로 통신하고, HTML 문서나 파일을 출력하는 GUI 기반의 소프트웨어
- 인터넷의 컨텐츠를 검색 및 열람하도록 함
- '웹 브라우저'라고도 함
- 주요 브라우저
  - Chrome, Firefox, Edge

### JS의 필요성

- 브라우저 화면을 동적으로 만들기 위함
- 브라우저를 조작할 수 있는 유일한 언어



## DOM(Document Object Model)

- DOM 조작
  - 문서(HTML)조작
- BOM 조작
  - navigator, screen, loacation, frames, histroy, XHR
- JavaScript Core
  - Data Structure, Conditional Expresstion



### DOM 이란?

- HTML, XML과 같은 문서를 다루기 위한 문서 프로그래밍 인터페이스
- 문서를 구조화하고 구조화된 구성 요소를 하나의 객체로 취급하여 다루는 논리적 트리 모델
- 문서가 구조화되어 있으며 각 요소는 객체로 취급
- 단순한 속성 접근, 메서드 활용뿐만 아니라 프로그래밍 언어적 특성을 활용한 조작 가능
- 주요 객체
  - window: DOM을 표현하는 창, 가장 최상위 객체(생략 可)
  - document: 페이지 컨텐츠의 Entry Point 역할, <body> 등과 같은 수많은 다른 요소들을 포함
  - navigator, location, history, screen

### 파싱(Parsing)

- 구문 분석, 해석
- 브라우저가 문자열을 해석하여 DOM Tree로 만드는 과정



### BOM이란?

- Browser Object Model
- 자바스크립트가 브라우저와 소통하기 위한 모델
- 브라우저의 창이나 프레임을 추상화해서 프로그래밍적으로 제어할 수 있도록 제공하는 수단
  - 버튼, URL 입력창, 타이틀 바 등 브라우저 윈도우 및 웹 페이지 일부분을 제어 가능
- Window 객체는 모든 브라우저로부터 지원받으며 브라우저의 창을 자칭



## 조작

### DOM 조작

1. 선택
2. 변경

- EventTarget
  - Event Listener를 가질 수 있는 객체가 구현하는 DOM 인터페이스
- Node
  - 여러가지 DOM 타입들이 상속하는 인터페이스
- Element
  - Document 안의 모든 객체가 상속하는 가장 범용적인 기반 클래스
  - 부모인 Node와 그 부모인 EventTarget의 속성을 상속
- Document 
  - 브라우저가 불러온 웹 페이지를 나타냄
  - DOM 트리의 진입점 역할을 수행
- HTMLElement
  - 모든 종류의 HTML요소
  - 부모 element의 속성 상속

### 선택관련 메서드

- Document.querySelector(selector)
  - 제공한 선택자와 일치하는 element 하나 선택
  - 제공한 CSS selector를 만족하는 첫번째 element 객체를 반환(없다면 null)
- Document.querySelectorAll(selector)
  - 제공한 선택자와 일치하는 여러 element 선택
  - 매칭할 하나 이상의 셀렉터를 포함하는 유요한 CSS selector를 인자로 받음
  - 지정된 셀렉터에 일치하는 NodeList를 반환



- getElementById(id)
- getElementByTagName(name)
- getElementByClassName(names)



### 변경관련 메서드

- Document.createElement()
  - 작성한 태그 명의 HTML 요소를 생성하여 반환
- Element.append()
  - 특정 부모 Node의 자식 NodeList 중 마지막 자식 다음에 Node 객체나 DOMString을 삽입
  - 여러 개의 Node객체, DOMString을 추가할 수 있음
  - 반환 값이 없음
- Node.appendChild()
  - 한 Node를 특정 부모 Node의 자식 Nodelist 중 마지막 자식으로 삽입
  - 한번에 오직 하나의 Node만 추가할 수 있음
  - 주어진 Node가 이미 문서에 존재하는 다른 Node를 참조한다면 새로운 위치로 이동

> append()를 사용하면 DOMString  객체를 추가할 수 있지만, appendChild()는 Node만 객체만 허용
>
> append()는 반환 값 있음, appendChild()는 추가된 Node 객체를 반환
>
> append()는 여러 Node 객체와 문자열 추가, appendChild() 하나의 Node 객체만 추가



### 변경관련 속성

- Node.innerText
  - Node 객체와 그 자손의 텍스트 컨텐츠를 표현
  - 즉, 줄 바꿈을 인식하고 숨겨진 내용을 무시하는 등 최종적으로 스타일링이 적용된 모습으로 표현
- Element.innerHTML
  - 요소 내에 포함된 HTML 마크업을 반환
  - XSS 공격에 취약
  
  

### 삭제관련 메서드

- ChildNode.remove()
  - Node가 속한 트리에서 해당 Node를 제거
- Node.removeChild()
  - DOM에서 자식 Node를 제거하고 제거된 Node를 반환
  - Node는 인자로 들어가는 자식 Node의 부모 Node



### 속성관련 메서드

- Element.setAttribute(name, value)
  - 지정된 요소의 값을 설정
  - 속성이 이미 존재하면 값을 갱신, 존재하지 않으면 지정된 이름과 값으로 새 속성을 추가
- Element.getAttribute(attributeName)
  - 해당 요소의 지정된 값을 반환
  - 인자는 값을 얻고자 하는 속성의 이름



## EVENT

### EVENT

- 네트워크 활동이나 사용자와의 상호작용 같은 사건의 발생을 알리기 위한 객체
- 이벤트 발생
  - 마우스를 클릭하거나 키보드를 누루는 등 사용자 행동으로 발생
  - 특정 메서드를 호출하여 프로그래밍 적으로도 만들어 낼 수 있음



### EVENT HANDLER

- EventTarget.addEventListener(type, listner[, options])

  - "특정 이벤트가 발생하면 할 일을 등록하자!"

  - 지정한 이벤트가 대상에 전달될 때마다 호출할 함수를 설정
  - 이벤트를 지원하는 모든 객체를 대상으로 지정 가능

- type

  - 반응 할 이벤트 유형(대소문자 구분)

- listener

  - 지정된 타입의 이벤트가 발생했을 때 알림을 받는 객체
  - EventListner 인터페이스 혹은 JS function 객체여야함

### EventTarget

- Event Listener를 가질 수 있는 객체가 구현하는 DOM 인터페이스



### 이벤트 취소

- Event.preventDefault()
- 현재 이벤트의 기본 동작을 중단
- 태그의 기본 동작을 작동ㄹ하지 않게 막음
  - a 태그의 기본 동작은 클릭시 링크로 이동 / form태그의 기본 동작은 form 데이터 전송

