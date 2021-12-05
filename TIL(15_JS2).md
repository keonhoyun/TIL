# TIL_JavaScript 2

## ECMA

- 정보통신에 대한 표준을 제정하는 비영리 표준화 기구
- ECMAScript는 ECMA-262 규격에 따라 정의한 언어



## 변수와 식별자

- 식별자는 변수를 구분할 수 있는 변수명
- 식별자는 문자, 달러($), 밑줄(_)로 시작
- 대소문자 구분, 클래스명 이외는 모두 소문자
- 예약어(for, if, case) 사용불가



### 카멜 케이스(camelCase)

- 변수, 객체, 함수에 사용



### 파스칼 케이스(PascalCase)

- 클래스, 생성자에 사용



### 대문자 스네이크 케이스(SNAKE_CASE)

- 상수에 사용



### 변수 선언 키워드(let, const)

#### let

- 재할당 가능
- 재선언 불가능
- *블록 스코프

*if, for, 함수 등의 중괄호 내부를 가리킴,

*블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능



#### const

- 재할당 불가능
- 재선언 불가능
- 블록 스코프



#### VAR

- 재선언, 재할당 모두 가능
- 호이스팅 되는 특성으로 예기치 못한 문제 가능 - 변수를 선언 이전에 참조할 수 있는 현상 / 변수 선언 이전의 위치에서 접근시 undefined를 반환
- 함수 스코프 - 함수의 중괄호 내부를 가리킴, 바깥에서 접근 불가



## 데이터 타입

### 원시타입

- 객체가 아닌 기본 타입
- 변수에 해당 타입의 값이 담김
- 다른 변수에 복사할 때 실제 값이 복사됨



#### 숫자타입

- 정수, 실수 구분 X
- 부동소수점
- 계산 불가시 NaN 반환



#### 문자열 타입

- 텍스트 데이터를 나타냄
- 16비트 유니코드
- 작은따옴표, 큰 따옴표 모두 사용 가능
- `사용 ${}와 형태로 표현



#### undefined  / null

- undefined : 빈 값 표현, 아무 값도 할당 안 하면 JS가 자동으로 할당, typeof의 결과는 undefined
- null : 빈 값을 표현, 개발자가 의도적으로 필요한 경우 할당, typeof의 결과값은 object



#### Boolean

- 논리적 참,거짓
- true or false
- 조건문 or 반복문



### 참조타입

- 객체 타입의 자료형
- 변수에 해당 객체의 참조값이 담김
- 다른 변수에 복사할 때 참조값이 복사됨



## 연산자

### 할당 연산자

- 오른쪽에 있는 피연산자의 평가 결과값을 왼쪽 피연산자에 할당하는 연산자
  - ex) +=, -=, *=, /=, ++, --

### 비교 연산자

- 피연산자들을 비교하고 결과값을 boolean으로 반환
- 알파벳의 경우 순서가 뒤에 있는 글자가 큼, 소문자가 대문자보다 큼



### 동등비교 연산자(==)

- 같은 값으로 평가되는지 판단
- 암묵적 타입 변환

``` javascript
const a = 1004
const b = '1004'
console.log(a==b) // true

const c = 1
const d = true
console.log(c==d) // true
```



### 일치비교 연산자(===)

- 엄격한 비교, 암묵적 변환 X

```javascript
const a = 1004
const b = '1004'
console.log(a==b) // false

const c = 1
const d = true
console.log(c==d) // false
```



### 논리 연산자

- and = &&
- or = ||
- not = !

- 단축평가 지원
  - false && true => false
  - true || false => true



### 삼항연산자

- 세 개의 피연산자 사용 조건에 따라 반환
- 가장 왼쪽의 조건식이 참이면 콜론 앞의 값 사용, 그렇지 않으면 뒤의 값

```javascript
console.log(true ? 1 : 2) // 1
console.log(false ? 1 : 2) // 2

const result = Math.Pi > 4 ? 'Yes' : 'No'
console.log(result) // No
```



## 조건문

### If 

- 조건 표현식의 결과값을 Boolean 타입으로 변환 후 참 거짓 판단
- 조건은 소괄호 안에 작성
- 실행할 코드는 중괄호 안에 작성
- 블록 스코프 생성

```javascript
if (condition) {
    // do something
} else if (condition){
    // do something
} else {
    // do something
}     
```



```javascript
const nation - 'Korea'

if (nation == 'Korea') {
    console.log('안녕하세요')
} else if (nation == 'France') {
    console.log('Bonjour')
} else {
    console.log('Hello')
}
```



### Switch

- 조건식의 결과값이 어느 값에 해당하는지 판별
- 조건에 따라 분기  시 사용

- 표현식의 결과값과 case문의 오른쪽 값을 비교
- break default문은 선택적으로 사용 가능
- break문이 없는 경우 break문을 만나거나 default문을 실행할 때까지 다음 조건문 실행
- 블록 스코프

```javascript
switch(expression) {
    case 'first value': {
        // do something
        [break]
    }
    case 'second value': {
        // do something
        [break]
    }
    [default: {
     // do something
     }]
}
```

```javas
const nation == 'Korea'

switch(nation) {
case 'Korea': {
	console.log('안녕하세요')
	break
}
case 'France': {
	console.log('Bonjour')
	break
}
default: {
	console.log('Hello')
}
}

## break가 없으면 모두 출력함
```



## 반복문

### While

- 조건문이 참인 동안 반복 시행
- 조건은 소괄호에 작성
- 실행할 코드는 중괄호에 작성
- 블록스코프

```javascript
while (condition) {
    // do something
}
```

```javascript
let i = 0
while (i < 6) {
    console.log(i) // 0, 1, 2, 3, 4, 5
    i += 1
}
```



### for 

- 세미콜론으로 구분되는 세 부분으로 구성
-  initializatioin
  - 최초 반복문 진입 시 1회만 실행되는 부분
- condition
  - 매 반복 시행 전 평가되는 부분
- expression
  - 매 반복 시행 후 평가되는 부분

```javascript
for (initialization; condition; expression) {
    // do something
}
```



```javascript
for (let i = 0; i < 6; i++) {
    console.log(i) // do something
}
```



### for in(객체 순회)

- 객체의 속성들을 순회할 때 사용
- 배열 순회 가능(권장 X)
- 중괄호 안에 작성
- 블록 스코프

```javascript
for (variable in object) {
    // do something
}
```

```javascript
const capitals = {
    Korea: '서울',
    France: '파리',
    USA: '워싱턴 D.C.'
}

for (let capital in capitals) {
    console.log(capital)
}
```



### for of(배열 원소 순회)

- 반복 가능한 객체를 순회
- 중괄호 안에 작성
- 블록 스코프 생성

```javascript
for (variable in iterable) {
    // do something
}
```

```javascript
const fruits = ['딸기', '바나나', '메론']

for (let fruit of fruits) {
    console.log(fruit)
}
```

