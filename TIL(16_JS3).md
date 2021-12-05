# TIL_JS3

## 함수 활용법

### 일급 객체

- 변수에 할당 가능
- 함수의 매개변수로 전달 가능
- 함수의 변환 값으로 사용 가능



### 함수 선언식

```javascript
function name(args) {
    // do something
}
```

```javascript
function add(numOne, numTwo) {
    return numOne + numTwo
}

const result = add(1, 2)
console.log(result) // 3
```

- 함수의 이름과 함께 정의하는 방식
- 3가지 부분으로 구성
  - 함수의 이름
  - 매개변수
  - 몸통



### 함수 표현식

```javascript
const muFunction = function (args) {
    // do something
}
```

```javascript
function add(numOne, numTwo) {
    return numOne + numTwo
}

const result = add(1, 2)
console.log(result) // 3
```

- 함수를 표현식 내에서 정의하는 방식
- 함수의 이름을 생략하고 익명 함수로 정의 가능
- 3가지 부분으로 구성
  - 함수의 이름(생략 가능)
  - 매개변수
  - 몸통



### 기본 인자(default arguments)

- 인자 작성 시 = 문자 뒤 기본 인자 선언 가능

```javascript
const greeting = function (name= 'noName') {
    console.log(`hi ${name}`)   
}

greeting() // hi noName
```



## 선언식 vs 표현식

|        | 함수 선언식                 | 함수표현식                |
| ------ | --------------------------- | ------------------------- |
| 공통점 | 데이터 타입, 함수 구성요소  | 좌동                      |
| 차이점 | 익명 함수 불가능, 호이스팅O | 익명 함수 가능, 호이스팅X |



### 함수의 타입

- 선언식 함수와 표현식 함수 모두 타입은 function으로 동일

```javascript
const add = function (args){ } // 함수 표현식

function sub(args) { } // 함수 선언식
```



### 호이스팅 - 함수 선언식

- 함수 호출 이후에 선언해도 동작

```javascript
add(2, 7) // 9

function add (num1, num2) {
    return num1 + num2
}
```



### 호이스팅 - 함수 표현식

- 함수 정의 전에 호출시 에러 발생

```javascript
sub(7, 2)

const sub = function (num1, num2) {
    return num1 - num2
}
```



## Arrow Functioin

### 화살표 함수

- 함수를 비교적 간결하게 정의할 수 있는 문법
- function 키워드 생략 가능
- 매개변수가 단 하나 뿐이라면 ()도 생략
- 몸통이 표현식 하나라면 {}, return 생략



```javascript
const arrow = function (name) {
    return `hellow! ${name}`
}

// function 키워드 삭제
const arrow = (name) => { return `hellow ${name}` }

// ()생략
const arrow = name => { return `hellow ${name}` }

// {}, return 생략
const arrow = name => `hellow ${name}`
```



## 배열

- 키와 속성들을 담고 있는 참조 타입의 객체
- 순서를 보장
- 주로 대괄호를 이용하여 생성하고, 0을 포함한 양의 정수 인덱스로 특정 값에 접근가능
- 배열의 길이는 array.length 형태로 접근 가능



### 주요 메서드

| 매서드          | 설명                                              | 비고                    |
| --------------- | ------------------------------------------------- | ----------------------- |
| reverse         | 원본 배열의 순서를 반대로 정렬                    |                         |
| push & pop      | 가장 뒤에 요소를 추가 또는 제거                   |                         |
| unshift & shift | 가장 앞에 요소를 추가 또는 제거                   |                         |
| includes        | 배열에 특정 값이 존재하는지 판별 후 참, 거짓 반환 |                         |
| indexOf         | 배열에 특정 값이 존재하는지 판별 후 인덱스 반환   | 요소 없을시 -1반환      |
| join            | 모든 요소를 구분자를 이용하여 연결                | 구분자 생략시 쉼표 기준 |



```javascript
const numbers = [1, 2, 3, 4, 5]
numbers.reverse()
console.log(numbers) // [5, 4, 3, 2, 1]
```



```javascript
const numbers = [1, 2, 3, 4, 5]

numbers.push(100)
console.log(numbers) // [1, 2, 3, 4, 5, 100]

numbers.pop()
console.log(numbers) // [1, 2, 3, 4, 5]
```



```javascript
const numbers = [1, 2, 3, 4, 5]

numbers.unshift(100)
console.log(numbers) // [100, 1, 2, 3, 4, 5]

numbers.shift()
console.log(numbers) // [1, 2, 3, 4, 5]
```



```javascript
const numbers = [1, 2, 3, 4, 5]

console.log(numbers.includes(1)) // true
console.log(numbers.includes(100)) // false
```



```javascript
const numbers = [1, 2, 3, 4, 5]
let result

result = numbers.indexOf(3) // 2
console.log(result)

result = numbers.indexOf(100) // -1
console.log(result)
```



```javascript
const numbers = [1, 2, 3, 4, 5]
let result

result = numbers.join() // 1, 2, 3, 4, 5
console.log(result)

result = numbers.join('') // 12345
console.log(result)

result = numbers.join(' ') // 1 2 3 4 5
console.log(result)

result = numbers.join('-') // 1-2-3-4-5
console.log(result)
```



### 주요 메서드2

- 배열을 순회하며 특정 로직을 수행하는 메서드
- callback함수를 받음
  - callback함수: 어떤 함수의 내부에서 실행될 목적으로 인자를 넘겨받는 함수

| 메서드  | 설명                                               |
| ------- | -------------------------------------------------- |
| forEach | 배열의 각 요소에 대한 콜백 함수를 한 번씩 실행     |
| map     | 콜백 함수의 반환 값을 요소로 하는 새로운 배열 반환 |
| filter  | 반환 값이 참인 요소들만 모아서 새로운 배열을 반환  |
| reduce  | 콜백 함수의 반호나 값들을 하나의 값에 누적후 반환  |
| find    | 반환 값이 참이면 해당 요소를 반환                  |
| some    | 요소 중 하나라도 판별 함수를 통과하면 참을 반환    |
| every   | 모든 요소가 판별 함수를 통과하면 참을 반환         |

#### forEach

```javascript
array.forEach((element, index, array) => {
    // do something
})
```

```javascript
const ssafy = ['광주', '대전', '구미', '서울']

ssafy.forEach((region, index) => {
    console.log(region, index)
})
// 광주 0
// 대전 1
// 구미 2
// 서울 3
# return 없음
```

#### map

```javascript
array.map((element, index, array) => {
    // do something
})
```

```javascript
const numbers = [1, 2, 3, 4, 5]

const doubleNums = numbers.map(num) => {
    return num*2
}
console.log(doubleNums) // [2, 4, 6, 8, 10]
```



#### filter

```javascript
array.filter((element, index, array) => {
    // do something
})
```

```javascript
const numbers = [1, 2, 3, 4, 5]

const oddNums = numbers.filter(num, index) => {
    return num % 2
}
console.log(oddNums) // [1, 3, 5]
```



#### reduce

```javascript
array.reduce((acc, element, index, array) => {
    // do something
}, initialValue)

// acc = 이전 callback함수의 반환 값이 누적되는 변수
// initialValue = 최초 callback함수 호출시 acc에 할당되는 값
```

```javascript
const numbers = [1, 2, 3]

const result = numbers.reduce((acc, num)) => {
    return acc + num
}, 0)

console.log(result) // 6
```

#### find

```javascript
arrays.find((element, index, array) => {
    // do something
})
```

```javascript
const averages = [
    { name: 'Tony Stark', age: 45 },
    { name: 'Steve Rogers', age: 32 },
    { name: 'Thor', age: 40 },
    
]

const result = averages.find((avenger) => {
    return avenger.name === 'Tony Stark'
})

console.log(result) // { name: 'Tony Stark', age: 45 }
```

#### some

```javascript
arrays.some((element, index, array) => {
    // do something
})
```

```javascript
const numbers = [1, 3, 5, 7, 9]

const hasEvenNumber = numbers.some(num) => {
    return num % 2 === 0
})
console.log(hasEvenNumber) // false

const hasEvenNumber = numbers.some(num) => {
    return num % 2
})
console.log(hasEvenNumber) // true
```

#### every

```javascript
arrays.every((element, index, array) => {
    // do something
})
```

```javascript
const numbers = [2, 4, 6, 8, 10]

const isEveryNumberEven = numbers.some(num) => {
    return num % 2 === 0
})
console.log(isEveryNumberEven) // true

const isEveryNumberEven = numbers.some(num) => {
    return num % 2
})
console.log(isEveryNumberEven) // false
```



## 객체

### 정의

- 속성의 집합, 중괄호 내부에 key와 value의 쌍으로 표현
- key는 문자열 타입만 가능
- value는 모든 타입 가능
- 요소 접근은 대괄호로 가능 or .으로 가능

```javascript
const me = {
    name: '홍길동', // key가 한 단어일 때
    'phone number': '01012345678',
    samsungProducts: {			// 여러 단어 일때
        buds: 'Galaxy Buds Pro',
        galaxy: 'Galaxy S21',
    },
}

console.log(me.name)
console.log(me['phone number'])
console.log(me.samsungProducts)
console.log(me.samsungProducts.buds)
```



### 문법 익히기

#### 속성명 축약

- key와 할당하는 변수의 이름이 같으면 축약 가능

```javascript
let books ['Learning Js', 'Eloquent JS']
let megazines = null

const bookShop = {
    books: books,
    magazines: magazines
}

console.log(bookShop.books)

## 축약형
let books ['Learning Js', 'Eloquent JS']
let megazines = null

const bookShop = {
    books,
    magazines,
}

console.log(bookShop.books)

```



#### 메서드명 축약

```javascript
const obj = {
    greeting: function () {
        console.log('Hi!')
    }
};

obj.greeting()

### 축약형

const obj = {
    greeting() {
        console.log('Hi!')
    }
};

obj.greeting()
```



#### 계산된 속성

```javascript
const key = 'regions'
const value = ['광주', '대전', '서울']

const ssafy = {
    [key]: value,
}

console.log(ssafy) // {regions: Array(4)}
console.log(ssafy.regions) // ['광주', '대전', '서울']
```



#### 구조분해 할당

```javascript
const userInformatioin = {
    name: 'ssafy kim',
    userId: 'ssafyStudent1234',
    phoneNumber: '010-1234-1234',
    email: 'ssafy@ssafy.com'
}

const name = userInformatioin.name
const userId = userInformatioin.userId
const phoneNumber = userInformatioin.phoneNumber

### 축약형
const userInformatioin = {
    name: 'ssafy kim',
    userId: 'ssafyStudent1234',
    phoneNumber: '010-1234-1234',
    email: 'ssafy@ssafy.com'
}

const { name } = userInformatioin
const { userId } = userInformatioin
const { phoneNumber } = userInformatioin
const { name, phoneNumber } = userInformatioin



```



