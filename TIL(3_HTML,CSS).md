# :page_facing_up: TIL HTML

## :star: :star: :star:

1. 공식문서 읽기
2. 영어 문서 읽기
3. 검색 내용 정리하기

## :computer: WEB 들어가기

- 현재의 웹표준 : W3C - HTML5  VS  WHATWG - HTML Living Standard
- WHATWG가 승리 

## :desktop_computer: HTML

- Hyper Text Markup Language
- Hyper : 동일선상에 있는 것이 아니라 다중으로 연결되어 있는 상태
- Hyper Text : 다른 문서로 즉시 접근할 수 있는 텍스트 / 선형적인 텍스트가 아닌 비 선형적으로 이루어진 텍스트, 인터넷과 함께 대두됨, 기본적으로 Hyper Link를 통해 텍스트 이동
- Markup : 텍스트의 역할을 부여함 (큰 제목, 작은 제목.....)
- Markup Language: 
  - 태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어,
  - 데이터를 단순히 표현하기만 함
  - 웹 컨텐츠의 의미와 구조를 정의 ex) HTML, Markdown

### HTML 기본구조

```html
<!DOCTYPE html>
<!-- html 요소 = 최상위 요소 / 문서의 root를 뜻함-->
<!-- head와 body 부분으로 구분-->
<html lang="ko">
<!--head 요소 = 문서제목, 문자코드(인코딩 등) 해당 문서의 정보를 담고 있음-->
<!--브라우저에 나타나지 않음-->
<!--CSS 선언 혹은 외부 로딩파일 지정 등도 작성-->
<!--메타 데이터를 표현하는 새로운 규약 Open Graph Protocal-->
<!--카톡에서 링크 보내면 썸네일 처럼 보여지는 것 Facebook 製作-->
<head>  
    <meta charset="UTF-8">
    <title>Document</title>  
    </head>
<!--body 요소 = 사용자에게 보여짐 / 실제 내용에 해당함-->
<body>    
    </body>
</html>
```

### DOM (Document  Object  Model) 트리

- 부모 관계 / 형제 관계
- 파이썬은 4Space 지만 HTML은 2Space -> 보기가 편하기 때문
- DOM은 문서의 구조화된 표현을 제공 
- 프로그래밍 언어가 DOM구조에 접근할 수 있는 방법을 제공
- Web Page의 객체 지향 표현

### 요소

- HTML의 요소는 태그와 내용으로 구성되어 있다.

```html
<h1> ---- 여는.시작 태그
    
</h1>---- 닫는/종료 태그
```

- 시작 태그 / 종료 태그 / 태그 사이에 위치한 내용으로 구성
  - 태그는 컨텐츠를 감싸는 것으로 그 정보의 성격과 의미를 정의
- 요소는 중첩 가능(nested)
  - 요소의 중첩을 통해 하나의 문서를 구조화
  - 여는 태그와 닫는 태그의 쌍을 잘 확인!
- 내용이 없는 태그 
  - br, hr, img, input, link, meta

### 속성

- <a href="https://~~~~"
- href = 속성명 / https ~~ : 속성값
- 붙여쓰기!! / ""(쌍 따옴표) 쓰기!
- 속성을 통해 태그의 부가적인 정보를 설정할 수 있음
- 경로나 크기와 같은 추가적인 정보 제공 가능
- 요소의 시작태그에 작성 / 이름과 값이 하나의 쌍으로 존재
- 태그와 상관없이 가능한 속성 有

### 공통속성

- id, class - id : 문서 전체에서 유일해야하는 고유식별자(id) 정의
- hidden - 해당요소가 관련이 없음 / 자리는 차지하지만 보이지 않음
- lang - 요소의 언어를 정의
- style - css스타일 선언
- tabindex
- title - 요소에 대한 추가정보

### 시맨틱 태그

- header - 문서 전체나 섹션의 헤더(머릿말)
- nav - 내비게이션
- aside - 사이드에 위치한 공간, 메인 컨텐츠와 관련성이 적은 컨텐츠
- section - 문서의 일반적인 구분, 컨텐츠의 그룹을 표현
- article - 문서, 페이지, 사이트 안에서 독립적으로 구분되는 영역
- footer - 문서 전체나 섹션의 푸터(마지막 부분)
- div, span은 Non semantic이지만 h1, table은 시멘틱으로 볼 수 있음
- 가독성을 높이고 유지보수에 유리 -> 메타태그, 시멘틱 태그 등을 통해 마크업을 효과적으로 작성

### 시맨틱 웹

- 웹 상에 존재하는 수많은 웹 페이지들에 메타데이터 부여
- 단순한 데이터 집합이었던 웹페이지를 의미와 관련성을 가지는 거대한 데이터베이스로 구축

### 문서구조화

- 그룹 컨텐츠

  - < p > 문단

  - < hr >  헤드라인
  - < ol > 순서가 있는 리스트 / < ul > 순서가 없는 리스트

- 텍스트 관련 요소

  - < a > 하이퍼 텍스트
  - < b > / < strong > 굵게
  - < i > / < em > 이탤릭
  - < span > 구조잡기 = < div >
  - < br > 줄바꿈

- form  태그 -  서버에서 처리될 데이터를 제공하는 역할

  - action 어디로 보낼지
  - method 

- input 태그 다양한 타입을 가지는 입력 데이터

  - < label > 서식 입력 요소의 캡션
  - < input > 공통 속성
    - name, placeholder
    - required
    - autofocus
    - ↑ 요소들은 type에 따라 달라짐

## :notebook_with_decorative_cover: 마크업해보기

```html
<header>
    <!-- 링크 적용하기 / 이미지와 연결-->
    <a href='https://www.ssafy.com/'>
    <!-- 이미지 불러오기, alt는 이름 설정 = 음성으로 읽을 때 해당 이름 불러줌-->
    	<img src="ssafy.png" alt="main img" width='300'>
    </a>
    <h1>SSAFY 학생 건강설문</h1>
</header>
```

```html
<section>
    <!-- #에 주소를 입력하면 해당 서버로 데이터를 보냄-->
	<form action="#">
    <!-- 이름칸이 들어올 자리-->
    <!-- 지역칸이 들어올 자리-->
    <!-- 체온칸이 들어올 자리-->
    <!-- 제출(submit)버튼 생성 / 제출이라는 이름으로 보이기-->
        <input type="submit" value="제출">
    </form>
</section>
```

```html
<div>
    <!-- 이름을 기재해주세요 보이기 / for은 해당 id와 연결 = 클릭하면 해당 요소로 포인터 이동-->
    <lavel for="name">이름을 기재해주세요</lavel><br>
    <!-- br은 줄바꿈, text입력할 수 있는 type생성, id 입력(연결), 이름은 안겹치는 것이 좋음, 사이트 접속하면 자동으로 포커싱되기(autofocus)-->
    <input type='text' id="name" name="name" autofocus>
</div>
```

```html
<div>    
    <label for="region">지역을 선택해 주세요.</label><br>
    <!-- 선택 리스트 만들기, 필수로 선택하도록 하기(=requried)-->
    <select name="region" id="region" required>
        <option value="">선택</option>
        <option value="서울">서울</option>
        <option value="대전">대전</option>
    <!-- 선택할 수 없게 하기 / 눈에 보이기는 함 / 약간 흐리게 보임-->
        <option value="강원" disabled>강원</option>
    </select>
</div>
```

```html
<div>
    <p>오늘의 체온을 선택하세요</p>
    <!-- 라디오버튼 생성 / id와 라벨의 for 연결 / 기본값으로 설정(=checked)-->
    <input type="radio" name="body-heat" id="normal" value="normal" checked>
    <label for="normal">37도 미만</label><br>
    <input type="radio" name="body-heat" id="warning" value="warning">
    <label for="warning">37도 이상</label>
    
</div>
```



# :page_facing_up: TIL CSS

## :computer_mouse: CSS

### CSS

- 스타일, 레이아웃 등을 통해 문서를 표시하는 방법을 지정하는 언어
- 선택자와 함께 열림
- 선택자를 통해 스타일을 지정할 HTML요소 선택
- 중괄호 안에는 속성과 값, 하나의 쌍으로 이루어진 선언을 진행 => 속성 + 값 = 선언
- 속성 = 어떤 스타일 기능을 변경할지 결정
- 값 = 어떻게 스타일 기능을 변경할지 결정

```css
# h1 = 선택자
h1 {
<!--선언-->
    color: blue;
<!-- font-size = 속성-->
<!-- 15px = 값-->
    font-size: 15px;
}
```

```html
<!--인라인 - 해당 태그에 직접 style 속성 활용-->
<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset="UTF-8">
    <meta name="viewpoint" content="width=device-width, initial-scale=1.0">
    <title>Doument</title>    
    </head>
<body>
    <h1 style="color: blue; font-size: 100px;">Hello</h1>
    </body>
</html>
```

```html
<!--인라인2 - head태그 내에 style 지정-->
<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset="UTF-8">
    <meta name="viewpoint" content="width=device-width, initial-scale=1.0">
    <title>Doument</title>
    <stlye>
        h1 {
          color: blue;
          font-size: 100px;
        }
    </stlye>
    </head>
<body>    
</html>
```

```html
<!--외부참조 head내 link를 통해 불러오기-->
<!DOCTYPE html>
<html lang='en'>
<head>
    <title>mySite</title>
    <link rel="stylesheet" href="mystlye.css">
    </head>
<body>
    <h1>This is my site</h1>
</body>
</html>
```

```css
<!--외부참조할 파일-->
h1 {
    color: blue;
    font-size: 20px
}
```



### 선택자

- HTML문에서 특정한 요소를 선택하여 스타일링 하기 위해서는 반드시 선택자라는 개념이 필요하다.
- 기본선택자
  - 전체 선택자, 요소 선택자
  - 클래스 선택자, 아이디 선택자, 속성 선택자
- 결합자
  - 자손 결합자, 자식 결합자
  - 일반 형제 결합자, 인접 형제 결합자

```css
/* 전체 선택자 */
* {
    color: red;
}

/* 요소 선택자 */
/* 태그를 직접 선택 */
h1 {
    color: orange;
}
h3,
h4 {
    color: red;
}

/* 클래스 선택자 */
/* 해당 클래스가 적용된 모든 항목 선택 */
.gren {
    color: green;
}

/* id 선택자 */
/* 해당 아이디가 적용된 모든 항목 */
/* 일반적으로 하나의 문서에 1번만 사용 */
/* 단일 id 사용권장(중복X) */
#purple {
    color: purple
}

/* 자식 선택자 */
/* 바로 아래의 요소 하나만 */
.box > p {
    font-size: 100px;
}

/* 자손 선택자 */
/* 하위 모든 요소 */
.box p {
    color: blue;
}

/* 일반 형제 */
/* 특정 요소 뒤 모든 해당 요소 선택 */
p ~ span {
    color: red;
}

/* 인접 형제 */
/* 바로 뒤에 위치하는 요소만 */
p + span {
    color: red;
}

/* 우선순위 */
/* 1. !important */
/* 2. 인라인 > id 선택자 > class 선택자 > 요소 선택자 */
/* 3. 소스 순서 */

```



### 상속

부모의 적용된 스타일을 자신이 물려받음(모두 x)

주로 text와 관련된 요소 상속

box모델 관련 postion관련 요소는 상속 x

```css
<style>
p {
    /* 상속됨 */
    color: red;
    /* 상속 안됨 */
    border: 1px solid black;
}

span {
    border: 1px solid blue;
}
</style>
```

### 크기단위

- px(픽셀)
  - 모니터 해상도의 한 화소인 픽셀 기준
  - 고정단위
- %
  - 백분율 단위
  - 가변적인 레이아웃
- em
  - 상속에 영향받음
  - 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈
- rem
  - 상속에 영향 X
  - 최상위 요소의 사이즈 기준
- viewport
  - 유저에게 바로 보이게 되는 웹 컨텐츠의 영역
  - 디바이스 별로 상대적인 사이즈 결정
  - vw, vh, vmin, vmax

### 색상단위

- 대소문자 구분X
- red, blue 등 직접 입력
  - RGB
    - 16진수 함수형 표기법
  - HSL
    - 색상, 채도, 명도 활용

## :package: Box Mdel

### BOX

- 모든 HTML은 box 형태로 구성
- 네 부분(영역)으로 구성
  - content - 실제 내용이 위치
  - padding - 테두리 안쪽 내부 여백
  - border - 태두리 영역
  - margin - 테두리 바깥의 외부 여백, 배경색 지정 不可
    - margin-top: 10px; / margin-right ......
    - margin: 10px; - 상하좌우 모두 10px
    - margin: 10px, 20px; - 상하 10px, 좌우 20px
    - margin: 10px, 20px, 30px; - 상 10px, 좌우 20px, 하 30px
    - border, padding 모두 동일
    - 기본값은 content로 크기 설정 -> box-sizing border-box로 설정 必

### 마진상쇄

- 둘 중에서 큰 마진 값으로 결합

### Display

- display: block;
  - 줄 바꿈이 일어남
  - 화면 크기 전체의 가로 폭 차지
  - 블록 레벨 안에 인라인 레벨 요소 삽입 可能
  - ex) div / ul, ol, li / p / hr / form 등
- display: inline;
  - 줄 바꿈이 일어나지 않음
  - content너비만큼 차지
  - width, height, margin-top, margin-bottom 지정 不可
  - 상하 여백은 line-height로 지정
  - ex) span  / a / img / input, label / b, em, i, strong 등
- display: inline-block;
  - block과 inline 요소 특징 모두 有
  - 한 줄 표시 可能
  - width, height, margin 속성 지정 可能
- display: none;
  - 해당 요소를 화면에 표시하지 않는다. (공간조차 사라진다.)
  - != visibility: hidden; -> 공간은 차지하나 화면 표시X

### 수평정렬

- margin-right: auto; (블록요소) == text-align: left; (인라인)
- margin-left; auto; (블록요소) == text-aligh; right; (인라인)
- margin-right: auto; < br > margin-left: auto;(블록) == text-align: center; (인라인)
