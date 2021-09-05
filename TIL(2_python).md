# :page_facing_up: TIL0726 

- 순서가 있는 데이터 구조
  - 문자열 / 리스트

- 순서가 없는 데이터 구조

  - 세트 / 딕셔너리

  

## 메서드

- .find(x)
  - x의 첫 번째 위치를 반환 / **없으면 -1을 반환**

- .index(x)

  - x의 첫 번째 위치를 반환 / **없으면 에러 발생**

- .replace(old, new[, count])
  - 바꿀 대상을 새로운 글자로 바꿔서 변환 / count를 지정하면 해당 개수만큼만 시행
  
- .strip([chars])

  - 특정문자를 지정하면 양쪽 or 왼쪽(lstrip) or 오른쪽 (rstrip) 제거/ 지정안하면 공백 제거 / \n, \t도 제거
  - 주로 사용자 입력을 받을 때 사용

- 'separator'. join([iterable])

  - 반복가능한 컨테이너 요소들을 separator(구분자)로 합쳐 문자열 반환

  - iterable이 str이어야하함 --> 아니면 error

    ex) '!'.join('ssafy') ---> s!s!a!f!y

    ​	  ' '.join(['3', '5']) -----> '3 5'

- .captitalize() : 앞글자를 대문자로

  . title(): '나 공백 이후를 대문자로 / 첫글자도 대문자

  .upper(): 모두 대문자로

  .lower(): 모두 소문자로

  .swapcase(): 대<->소문자로 변경

## 리스트

- 변경가능
- 순서있음
- 순회가능

### 리스트 메서드

- .extend(iterable)
  - 리스트에  iterable의 항목을 추가함
- .insert(i, x)
  - 정해진 위치 i에 x를 추가함 -> 리스트의 길이보다 클 경우 맨 뒤
- .remove(x)
  - 리스트에서 값이 x인 것 삭제 / **없는 경우 ValueError**
- .pop(i)
  - 정해진 위치 i에 있는 값을 삭제하고, 그 항목을 반환함 / **정해지지 않으면 마지막 항목**

- .clear()
  - 모든 항목 삭제
- .index(x)
  - x값을 찾아 해당 값의 index값을 반환

# :page_facing_up: ​ TIL 0727

## 모듈

- 특정 기능을 파이썬 파일(,py) 단위로 작성한 것

  - import로 불러와야함

    ex) import requests

## 패키지

- 모듈의 집합
- 패키지 안에는 또 다른 서브 패키지를 포함
  - pip install 패키지명 (==버전) / **작성안하면 최신파일**
  - pip uninstall 패키지명 ->  패키지 삭제 / 업그레이드 시 과거버전 자동 삭제
  - pip list -> 설치된 패키지 목록
  - pip show  패키지명 -> 자세히 들여다 보기
  - pip freeze -> pip list의 결과(파이썬 환경에 대한 정보)를 **requirements.txt로 만들어 관리**
    - $ pip freeze > requirements.txt (전부입력)
    - $ pip install  -r requirements.txt (requirements  속 패키지 설치하기)
  - pip install **-r** requirement.txt(파이썬 환경에 대한 정보를 바탕으로 재설치
- 패키지 집합 == 라이브러리

## 가상환경(venv)

- 복수 프로젝트를 할 시 버전이 상이할 수 있음  가상환경을 만들어 프로젝트별로 독립적인 패키지 관리 가능
- 특정 디렉토리(폴더)에 가상환경 만들고 고유한 파이썬 패키지 집합을 가질 수 있음
- 생성: python -m venv <폴더명> 
  - <폴더명>에 가상환경 정보가 들어있음
  - <폴더명>은 관습적으로 venv
    - $ python -m venv venv
- 활성화: source / 비활성화: deactivate
  - ex) git bash 사용시 : $ source venv/Scripts/activate
  - (venv) 표시가 나타남
  - 비활성화시 : $ deactivate

### sort 함수

 sorted(resverse='False')

ex) sorted(lotto, reverse = 'True')

---> 거꾸로 출력

# :page_facing_up: TIL 0728

## :question:

0726 homework 정사각형 넓이 set으로 변경 후 교집합 사용!!

교집합 & or intersection



## 클래스 변수

- 클래스 정의 안에 선언

- 특정 클래스 인스턴스에 묶여 있지 않음

- 클래스 자체의 내용을 저장

- 같은 클래스에서 생성된 모든 객체는 동일한 클래스 변수를 공유

  

## 인스턴스 변수

- 항상 특정 인스턴스에 묶여있음
- 클래스에 저장되지 않고 클래스에서 생성된 개별 객체에 저장
- 인스턴스 마다 완전히 독립적, 값을 수정하면 해당 객체에만 영향

```python
class Cat:
    num_tails = 1             # 클래스 변수
    
    def __init__(self, name): # 인스턴스 변수
        self.name = name
```

```python
alice = Cat('alice')
james = Cat('james')
print(alice.name) # alice
print(james.name) # james
print(alice.num_talis) # 1
print(james.num_tails) # 1
print(Cat.num_tails) # 1
```

- 그러나 클래스를 통해 인스턴스 변수에 접근할 수 없음

- 인스턴스 변수는 각 객체 인스턴스에 특정되고 init 생성자가 실행될 때 만들어짐

  - 클래스 자체에는 존재 x

    ```python
    print(Cat.name) # AttributeError
    ```

## 클래스 변수와 인스턴스 변수의 함정

```python
Cat.num_tails = 2
```

```python
print(alice.num_tails) # 2
print(james.num_tails) # 2
```

 

```python
Cat.num_tails = 1
```

```python
james.num_tails = 2
print(alice.num_tails) # 1
print(james.num_tails) # 2
print(Cat.num_tails) # 1 
## 클래스변수를 변겅한 것이 아닌 james인스턴스에 num_tails 인스턴스 변수가 생긴 것 / 이제 james는 클래스 변수에 접근 不可
```

- 클래스변수는 모든 클래스 인스턴스에서 공유하는 데이터를 위한 변수
- 인스턴스 변수는 각 인스턴스에 고유한 데이터를 위한 것
- 클래스 변수는 동일한 이름의 인스턴스 변수에 의해 가려질 수 있기 때문에 주의!



## 객체 비교

- == 
  - 동등한(equal)
  - 변수가 참조하는 객체가 동등한 경우 True
  - **두 객체가 같아 보이지만 실제로 동일한 대상을 가리키고 있다고 확인해준 것은 아님**
    - ex) 쌍둥이 고양이
- is
  - 동일한(identical)
  - 두 변수가 동일한 객체를 가리키는 경우 True

## 인스턴스 / 클래스 / 스태틱 매서드

- 인스턴스
  - self 매개 변수를 통해 동일한 객체에 정의된 속성 및 다른 메서드에 자유롭게 접근 가능
  - 클래스 자체에 접근할 수 있음
    - 즉, 인스턴스 메서드가 클래스 상태를 변경 可能
- 클래스 메서드
  - 클래스를 가리키는 cls 매게 변수를 받음
  - cls 인자에게만 접근 / 객체 인스턴스의 상태 수정 不可
- 스태틱 메서드
  - 임의 개수의 매개 변수를 받을 수 있지만, self나 cls 매개 변수는 사용하지 않음
  - 즉, 객체 상태나 클래스 상태 수정 不可
  - 일반 함수처럼 동작하지만 클래스의 이름공간에 귀속 됨

>**스태틱 메서드는 독립적으로 수행할 수 있음**
>
>**스태틱 메서드와 클래스 메서드는 개발자의 의도를 전달하기 위함임**
>
>**의도를 강제해 버그로 인해 설계를 깨드리지 않도록 함**
>
>**일반 함수를 사용하는 것처럼 실행할 수 있기 때문에 객제 지향 프로그래밍과 절차 지향 프로그래밍 스타일 사이를 연결하는 역할을 하기도 함**
>
>**코드 유지보수에 유리**

1

```python
class MyClass:
    def method(self):
        return 'instance method', self
    @classmethod
    def classmethod(cls):
        return 'class method', cls
    @staticmethod
    def staticmethod():
        return 'static method'
```



```python
obj = MyClass()

obj.method() # 'instance mmethod', <__main__.MyClass ~~~>
MyClass.method(obj) # 'instance method' ``
```



```python
obj.classmethod() # 'class method', __main__.MyClass
MyClass.classmethod() # 'class method', __main__.MyClass

obj.staticmethod() # 'static method'
```



## 상속

- 클래스는 상속이 가능함
  - 모든 파이썬 클래스는 object를 상속 받음
- 상속을 통해 객체 간의 관계를 구축
- 코드의 재사용성 高 

```python
class Person():
    def __init__(self, name, age, number, email):
               pass
class Professor(Person): # 자식 # 상속받은 상황
    pass
```

## 다중상속

```
class Person():
    def __init__(self, name):
               self.name = name
class Mom(Person):
    gene = 'XX'
    
    def swim(self):
    	return '첨벙첨벙'
    	
 class Dad(Person):
    gene = 'XY'
    
    def walk(self):
    	return '성큼성큼'
    	
  class FirstChild(Dad, Mom):
      def swim(self):
            return '챱챱'
            
      def cry(self):
    	return '응애'
   
   class SecondChild(Mom, Dad):
      def walk(self):
    	return '아장아장'
            
      def cry(self):
    	return '응애'   
```



```python
baby1 = FirstChild('하나')
baby2 = SecondChild('두리')
--------------------------
baby1.cry() # 응애
baby1.swim() # 챱챱
baby1.walk() # 성큼성큼
baby2.cry() # 응애
baby2.swim() # 첨벙첨벙
baby2.walk() # 아장아장
---------------------------
baby1.gene # 'XY' # Dad를 먼저 확인
baby2.gene # 'XX' # Mom을 먼저 확인
```



##  super()

- 상속할 때 같은 내용 받아오기

```python
class Person():
    def __init__(self, name, age, number, email):
                 self.name = name
                 self.age = age
                 self.number = number
                 self.email = email
                 
class Student(Person): # super()로 받아옴
     def __init__(self, name, age, number, email, student_id):
                 super().__init__(self, name, age, number, email)
                self.student_id = student_id
```



- 매서드 오버라이딩 
  - 상속받은 클래스에서 같은 이름의 메서드로 덮어씀
  - 부모 클래스의 메서드를 실행시키고 싶은 경우 super를 사용
- 상속관계에서 이름 공간은 인스턴스, 자식 클래스, 부모 클래스 순으로 탐색

```python
class Person():
    def __init__(self, name):
                 self.name = name
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')

class Professor(Person):
    def talk(self):
        print(f'{self.name}일세') # 김교수일세
        
class Student(Person):
    def talk(self):
        super().talk() 
        print(f'{self.name}일세') # 반갑습니다. 이학생입니다.
        					    # 저는 학생입니다.               
                 
```

- 파이썬의 모든 클래스는 object로부터 상속됨
- 부모 클래스의 모든 요소(속성, 메서드)가 상속됨
- super()를 통해 부모 클래스의 요소를 호출할 수 있음
- 메서드 오버라이딩을 통해 자식 클래스에서 재정의 가능함
- 상속관계에서의 이름 공간은 인스턴스, 자식 클래스, 부모 클래스 순으로 탐색

# :page_facing_up: TIL 0729

## 데이터 수집

- WWW : world wide web
- HTTP : HTML과 같은 리소스들을 가져올 수 있도록 해주는 프로토콜
- 클라이언트는 URL로 요청 / 서버는 문서(텍스트)를 응답

## Requests

- HTML을 받아오는 것까지 임무 수행

- $ pip install requests (설치)

```python
import requests # (불러오기)

response = requests.get('url') # (요청 보내기)

response.text  # 페이지 소스 받아오기 print(response.text)
```

## 크롤링

- 데이터 긁어오기
- 브라우저가 아닌 상황에서 필요 없는 데이터가 너무 많음
- 원하는 데이터를 얻기 위한 추가작업

## Beautiful Soup

- HTML에서 데이터를 뽑아주는 라이브러리
- $ pip install beautiuflsoup4

```python
from bs4 import BeautifulSoup # BeautifulSoup 클래스 꺼내기

data = BeautifulSoup(reponse.text, 'html.parser') # 본문 해석

kospi = data.select_one('원하는 곳 검사, 선택자 복사').text # 데이터 텍스트로 변환

print(kospi) # 3.224.26
```

## API

- 응용 프로그램을 위한 접점
-  API server : 응용 프로그램(개발자)를 위한 데이터를 응답하는 프로그램

```python
import requests
url = 'api 주소'

response = requests.get(url)

response.text # str 타입 / 눈에는 dict으로 보이지만 x / 코드 밖에서 가져온 데이터는 무조건 str

response = reqeusts.get(url).json() # json으로 parsing 필요

response['name'] # 키값 접근 가능
```

- ? : url과 parameter 구분
- & : parameter 와 parameter 구분

## API KEY값 숨기기

```bash
$ code ~/.bashrc
# 열고 신뢰누르기

export <api키 이름> = 'key'
터미널 종료 후 해당 파일에서
```

```python
import os 
API_KEY = os.getenv('api 키이름')
```

# :page_facing_up: TIL 0801

## 새로운 라이브러리

- from base64 import b64decode
- 







