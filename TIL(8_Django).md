# :page_facing_up: TIL_Django



## Static web page(정적 웹 페이지)

- 서버에 미리 저장된 파일이 사용자에게 그대로 전달되는 웹 페이지
- 서버가 정적 웹 페이지에 대한 요청을 받은 경우 서버는 추가적인 처리 과정 없이 클라이언트에게 응답을 보냄
- 모든 상황에서 모든 사용자에게 동일한 정보를 표시
- 일반적으로 HTML, CSS JavaScript로 작성됨
- flat page라고도 함



## Dynamic web page(동적 웹 페이지)

- 웹 페이지에 대한 요청을 받은 경우 서버는 추가적인 처리 과정 이후 클라이언트에게 응답을 보냄
- 동적 페이지는 방문자와 상호작용하기 때문에 페이지 내용은 그때 그때 다름
- 서버 사이드 프로그래밍 언어(python, java, c++등)가 사용되며 파일을 처리하고 데이터베이스와의 상호작용이 이루어짐



## Framework

- 프로그래밍에서 특정 운영 체제를 위한 응용 프로그램 표준구조를 구현하는 클래스와 라이브러리 모임
- 재사용할 수 있는 수많은 코드를 프레임워크로 통합함으로써 개발자가 새로운 애플리케이션을 위한 표준 코드를 다시 작성하지 않아도 같이 사용할 수 있도록 도움
- Apaplication Framwork라고도 함



## Web framework

- **<u>웹 페이지를 개발하는 과정에서 겪은 어려움을 줄이는 것이 주 목적</u>**
- 동적인 웹 페이지나, 웹 애플리케이션, 웹 서비스 개발 보조용으로 만들어지는 Application Framework의 일종



## MTV Pattern

- Model
  - 응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을 관리(추가, 수정, 삭제)
  - MVC Pattern의 model과 같다.

- Template
  - 파일의 구조나 레이아웃을 정의
  - 실제 내용을 보여주는 데 사용
  - MVC Pattern의 view와 같다.
- view
  - HTTP 요청을 수신하고 HTTP 응답을 반환
  - Model을 통해 요청을 충족시키는데 필요한 데이터에 접근
  - template에게 응답의 서식 설정을 맡김
  - MVC Pattern의 Controller와 같다.



## Django

```python
$ pip install django

$ django-admin startproject 프로젝트이름

$ python manage.py runserver

$ python manage.py startapp 앱이름
-> INSTALLED_APPS에 등록!
```



### 프로젝트 구조

- __ init __.py
  - python에게 이 디렉토리를 하나의 패키지로 다루도록 지시
- asgi.py
  - django 애플리케이션이 비 동기식 웹 서버와 연결 및 소통하는 것을 도움

- wsgi.py
  - django 애플리케이션이 웹서버와 연결 및 소통하는 것을 도움
- manage.py
  - Django 프로젝트와 다양한 방법으로 상호작용하는 커매드라인 유틸리티



### 애플리케이션 구조

- admin.py
  - 관리자용 페이지를 설정
- apps.py
  - 앱의 정보가 작성된 곳
- models.py
  - 앱에서 사용하는 Model을 정의
- tests.py
  - 프로젝트의 테스트 코드를 작성
- view.py
  - view 함수들이 정의됨



## URLS

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('movies/', include('movies.urls'))
]
```



## Views.py

```python
from django.shortcuts import render, redirect
from .models import Movie

def new(request):
    return render(request, 'movies/new.html')
```

## Templates

- 데이터 표현을 제어하는 도구이자 표현에 관련된 로직



### Django Template Language(DTL)

- django template에서 사용하는 built-in templatte system
- 조건, 반복, 변수 치환, 필터 등의 기능을 제공
- 파이썬과 구조가 비슷하지만, 파이썬 코드로 실행되는 것은 아님



- DTL Syntax_Variable

  - render()를 사용 -> templateㅍ 파일로 넘김
  - 변수명은 영어, 숫자와 밑줄 조합, 밑줄로 시작 不可
    - 공백과 구두점 문자 사용 不可
  - dot(.)을 사용하여 변수 속성에 접근
  - render()의 세번째 인자로 딕셔너리 형태로 넘겨줌, key값에 해당하는 문자열이  template에서 사용가능한 변수명

  

- DTL Syntax_Filters

  - 표시할 변수를 수정할 때 사용
    - name 변수를 모두 소문자로 출력
    - {{ name | lower}}
  - 60개의 built-in template filters를 제공
  - chained가 가능, 일부 필터는 인자를 받음
    - {{ variable|truncatewords:30 }}

  

- DTL Syntax_Tags

  - 출력 텍스트를 만들거나, 반복 또는 논리를 수행하여 제어 흐름을 만드는 등 변수보다 복잡한 일들을 수행
  - 일부 태그는 시작과 종료 태그가 필요



- DTL Syntax_Comments
  - django template에서 라인의 주석을 표현하기 위해 사용
    - {#   #}
  - 여러줄 주석은
    - {% comment %} {% endcomment %} 사이에 입력



### 템플릿 상속

- 템플릿 상속은 기본적으로 코드의 재사용성에 초점을 맞춤
- 템플릿 상속을 사용하며 사이트의 모든 공통요소를 포함
- base.html, 프로젝트와 같은 위치에 templates생성
- 중복을 배제하기 위해 한 고셍 저장하여 중복 배제
- 표현과 로직을 분리 템플릿은 표현을 제어하는 도구이자 표현에 관련된 로직일 뿐
- setting.py  속 TEMPLATES의 'DIRS' 에
  - [BASE_DIR / 'templates'] 작성



- tags
  - 자식 템플릿이 부모 템플릿을 확장한다는 것을 알림
  - 반드시 최상단에 작성
    - {% extends '' %}
  - 하위 템플릿에서 재지정할 수 있는 블록을 정의
  - 즉, 하위 템플릿이 채울 수 있는 공간
  - endblock 뒤 content는 선택요소
    - {% block content % }{% endblock (content) %}







## HTML Form

### form

- 웹에서 사용자 정보를 입력하는 여러 방식
- 핵심속성
  - action: 입력 데이터가 전송될 URL 지정
  - method: 입력 데이터 전달 방식 지정
    - GET(default)
    - POST
    - PUT
    - DELETE

### input

- 사용자로부터 데이터를 입력받기 위해
- type 속성데 따라 동작방식이 달라짐
- 핵심 속성
  - name
  - 중복가능, name이라는 이름에 설정된 값을 넘겨서 값을 가져옴
  - name은 key, value는 value
  - ?key=value&key=value형태로 전달

### label

- 사용자 인터페이스 항목에 대한 설명
- label을 input 요소와 연결
  - input에 id 속성 부여
  - label에는 input의 id와 동일한 값의 for 속성이 필요
- label과 input 요소 연결의 주요 이점
  - 시각적인 기능 뿐만 아니라 화면 리더기에서 label을 읽어서 사용자가 입력해야하는 텍스트가 무엇인지 더 쉽게 이해할 수 있도록 함
  - label을 클릭해서 input에 초점을 맞추거나 활성화 可能



#### for

- for 속성값과 일치하는 id를 가진 문서의 첫 번째 요소를 제어
  - 연결된 요소가 labelable element인 경우 이 요소에 대한 labeled control이 됨
- label 요소와 연결할 수 있는 요소
- button, input, select.....



## Variable Routing

- URL 주소를 변수로 사용하는 것
- URL일부를 변수로 지정하여 view 함수의 인자로 넘길 수 있음
- 즉, 변수 값에 따라 하나의 path()에 여러 페이지를 연결 可能



## URL Path converters

- str
  - /를 제외하고 비어 있지 않은 모든 문자열과 매치
- int 
  - 0 또는 양의 정수와 매치
- slug
  - ASCII 문자 또는 숫자, 하이픈 및 밑줄 문자로 구성된 모든 슬러그 문자열과 매치
  - ex) 'building-your-1st-django-site'

