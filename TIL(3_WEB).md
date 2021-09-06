# :page_facing_up: Web

## :desktop_computer: Web

### Float

- 한 요소가 정상 흐름으로부터 빠져 **<u>텍스트 및 인라인 요소</u>**가 그 주위를 감싸 요소의 좌, 우측을 따라 배치되어야 함을 지정
- 이미지를 한쪽으로 띄우고 텍스트를 둘러싸는 레이아웃을 위해 개발 ex) 신문, 잡지
  - 속성
    - none: 기본값
    - left: 요소를 왼쪽으로 띄움
    - right: 오른쪽으로 띄움

```html
<body>
    <div class="box left">float left</div>
    <p>lorem300 자동 완성으로 길게</p>
</body>
```

```css
.class {
    width: 150px;
}

.left {
    float: left;
}
```



- float clear
  - .classname::(::은 가상요소를 만드는 것) = 맨 마직막 자식으로 가상요소 생성
  - content속성과 짝지어 장식용 컨텐츠를 추가할 때 사용

```css
.clearfix::after{
      content: "";
    /* 기본값은 in line */
      display: block;
      clear: both;
    }
```



### Flexbox

요소

- Flex Container(부모 요소)
  - flex 레이아웃을 형성하는 기본적인 모델
  - 자식요소들이 놓여있는 영역
- Flex Item(자식 요소)
  - 컨테이너의 컨텐츠

축

- main axis (메인 축)
- cross axis (교차 축)

### justify-content

```html
<style>
/* flexbox 시작 */
/* 부모요소에 display: flex; or inline-flex를 작성하면서 시작 */
/* inline-flex는 요소만큼만 flex 지정*/
.flex-container {
  display: flex;
    
/* 배치방향 설정 - 기본값은 row 주축의 방향이 왼쪽->오른쪽 */
  flex-direction: row;
  /* 쌓이는 방향 반대 */ 
  flex-direction: row-reverse;
  /* 열방향(위쪽 -> 아래쪽)으로 쌓기 */ 
  flex-direction: column;
  /* 쌓이는 방향 반대 */
  flex-direction: column-reverse;
    
  /* 강제로 한 줄로 표시  */
  flex-wrap: nowrap;
  /* 벗어나면 한 줄 밑으로 이동 */
  flex-wrap: wrap;
  /* 벗어나면 한 줄 위로 이동 */
  flex-wrap: wrap-reverse;
    
  /* 방향과 랩의 short hand */  
  flex-flow: column wrap;
    
 /* 메인축 방향 설정 flex-direction: row;인 상황 */  
  /* content - 여러 줄 */
  /* items - 한 줄 */
  /* self - flex item 개별 요소 */
    
  /* 기본값 */
  justify-content: flex-start;
  /* 끝으로(오른쪽 끝) - row시 보내기 */
  justify-content: flex-end;
  /* 가운데 정렬 */
  justify-content: center;
  /* 좌우 정렬 - item간 간격 동일 */
  justify-content: space-between;
  /* 균등 좌우 정렬 - 내부 요소 공백이 외부의 2배 */
  justify-content: space-around;
  /* 균등 정렬 - 내부, 외부 요소 공백 동일 */
  justify-content: space-evenly;    
 }
</style>

```

 ### align

```html
<style>
.flex-container {
  display: flex;
  /* 교차축 정렬 flex-direction: row;인 상황 */
  
    /* 기본값 */
    align-items: stretch;
    
    /* 교차축기준 시작점(위) */
    align-items: flex-start;
    
    /* 교차축기준 가운데 */
    align-items: center;
    
    /* 교차축기준 끝(아래) */
    align-items: flex-end;
    
    /* 컨텐츠 크기를 기준 컨텐츠 바닥기준 정렬 */
    align-items: baseline;
    
    /* 상하좌우 가운데 정렬 */
    justify-content: center;
    align-items: center;
    
}
</style>
```

### align-self

```html
<style>
.flex-container {
  display: flex;
    
 }
.item1 {    
  /* 교차축 개별정렬 flex-direction: row;인 상황 */
    /* 교차축기준 시작점(위) */
    /* item1만 정렬 */
    
    /* 기본값 */
    align-self: auto;
    /* aling-items와 같음 */
    align-self: flex-start;
    /* 부모 컨테이너에 자동으로 맞춰서 늘어남 */
    align-self: stretch;
    
}
```

### order

```html
<style>
.flex-container {
  display: flex;
    
 }
/* order 값들의 순서 설정 */
    
.item1 {    
  /* 기본값 */
  order: 0;   
}
    
.item2 {    
  /* 앞으로 감 = 다른 값이 0이기 때문 */
  order: -1;   
}
.item3 {    
  /* 뒤로 감 = 다른 값이 0이기 때문 */
  order: 1;   
}
```

### flex-grow

```html
<style>
.flex-container {
  display: flex;
    
 }
/* grow 메인축에서 남은 공간을 숫자만큼 분배 */
/* 기본 값은 0 */
    
.item1 {    
  /* 남은 공간의 1/(1+2+3) */
  flex-grow: 1;   
}
    
.item2 {    
  /* 남은 공간의 2/(1+2+3) */
  flex-grow: 2;   
}
.item3 {    
  /* 남은 공간의 3/(1+2+3) */
  flex-grow: 3;   
}
```

# --------------------------------------



## :books: Bootstrap

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="bootstrap.css"
  <title>Document</title>
</head>
<body>
  <script src="bootstrap.bundle.js"></script>
</body>
</html>
```

### CDN

- Content Delivery Network
  - 컨텐츠를 효율적으로 전달하기 위해 여러 노드에 가진 네트워크에 데이터를 제공하는 시스템

### spacing

- 1 : 0.25 rem == 4px
- 2 : 0.5 rem == 8px
- 3 : 1 rem == 16px
- 4 : 1.5 rem == 24px
- 5 : 3 rem == 48px
- 0 : 0 rem == 0px

- m : margin
- p : padding

- t: top
- b : bottom
- s : left
- e : right
- x : left, right
- y : top, bottom

- fw : font-weignt -> bold / normal / light .....
- fst : font-style 

### Grid system

- flexbox로 제작
- container, rows, column으로 컨텐츠를 배치하고 정렬
- 반드시 기억해야할 2가지
  - 12개의 column
  - 6개의 grid breakpoints

```html
<!--계속 container 안에 작성해야 함-->
<div class='container'>
    <h2 class="text-center">alignment</h2>
    <div class="row justify-content-center align-items-center">
        <div class="col-4"></div>
        <div class="col-sm-6"></div>
        <div class="col-lg-3"></div>
    </div>
</div>
```

### Media Query

```html
<style>
    /* 700px보다 크다면 */
    @media (min-width: 700px) {
        h2 { color: red;}       
    }
    /* 500px보다 작다면 */
    @media (max-width: 500px) {
        h2 { color: blue;}
    }
    /* 가로이면 오리엔테이션 클래스 뒤에 컨텐츠 추가 */
    @mdeia (orientation: landscape) {
        p.orientation::after { content: '가로입니다.'}
    }
    /* 세로이면 오리엔테이션 클래스 p 뒤에 컨텐츠 추가 */
    @mdeia (orientation: portrait) {
        p.orientation::after { content: '세로입니다.'}
    }
</style>
```

### Font

```html
<!-- 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="bootstrap.css">
    -->
  <link href="여기에 링크 넣기">
<!-- 
  <title>Document</title>
</head>
<body>
  <script src="bootstrap.bundle.js"></script>
</body>
</html>
 -->
```

### Icon

- Bootstrap icon
- Font Awesome

```html
<body>
    <strong>'볼드체'</strong>
    <!--원래 이텔릭체 표시하는 i태그에 적기-->
    <!-- 사이트에서 검색 후 그대로 적용-->
    <i class="bi bi-vinal"></i>    
</body>
```

# -----------------------------------------

## :pen: CSS 톺아보기

### 우선순위

!important > 인라인 > #id선택자

> 위 3개는 쓰지말기! 자바스크립트에 양보!

> class > element > universal selector ( * ) 

> 명시도 점수에 따라 순서 정해짐, 점수가 같으면 마지막 스타일이 적용

### BEM

> Block, Element, Modifier
>
> Block - 혼자 독립적으로 존재 可能
>
> > ex) .form
>
> Element - 독립적으로 존재X, Block안에 있어야 의미를 가짐  "__"
>
> > ex) .form__group
>
> Modifier - 상태 바꾸기 " -- "
>
> > ex) .form--theme-xmas



```html
<style>
    /* 이것은 Block입니다. */
    .form {
        border: 3px solid black;
    }
    /* 이것은 Element입니다. */
    .form__group {
        margin-bottom: 1rem;
    }
    /* 부모기준 width 100%를 주어라 */
    .form__input {
        width: 100%;
    }
    /* 이것은 Modifier입니다. */
    .form--theme-xmas {
        background-color: green;
    }
</style>
```



```html
<body>
    <!-- form은 블록!-->
    <form class="form">
        <!-- 아래는 엘리먼트 -->
        <div class="form__group">
        <lavbel></lavbel>
        <input class="form__input">
    </div>        
    </form>    
</body>
```









