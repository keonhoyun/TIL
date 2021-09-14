# TIL_Django2

## Model

- 단일한 데이터에 대한 정보를 가짐
  - 사용자가 저장하는 데이터들의 필수적인 필드들과 동작들을 포함
- 저장된 데이터베이스의 구조
- model을 통해 데이터에 접속하고 관리
- 각각의 model은 하나의 데이터베이스 테이블에 매핑



## Database

- DB
  - 체계화된 데이터의 모임
- 쿼리
  - 데이터를 조회하기 위한 명령어
  - 조건에 맞는 데이터를 추출하거나 조작하는 명령어
- 스키마
  - 자료의 구조, 표현방법, 관계 등을 정의한 구조
- 테이블
  - 필드, <u>열</u>, 속성
  - 레코드, <u>행</u>, 튜블
- PK(기본키)
  - 각 행(레코드)의 고유값
  - 반드시 설정해야함, 관계설정시 주요하게 활용



## ORM

- Object-Relational-Mapping
- 객체 지향 프로그래밍 언어를 사용하여 호환되지 않는 유형의 시스템 간(Django-SQL)데이터를 변환
- 언어 간의 호환되지 않는 데이터를 변환하는 프로그래밍 기법
- 장점
  - SQL을 알지 못해도 DB조작 가능
  - 객체 지향적 접근으로 높은 생산성
- 단점
  - ORM만으로 완전한 서비스 구현 어려움



## Field

- CharField(max_length=None, **options)
  - 길이의 제한이 있는 문자열을 넣을 때
  - max_length는 필수 인자
  - 유효성 검사에서 활용
- TextField(**optioins)
  - 글자의 수가 많을 때 사용



## Migrations

- model에 생긴 변화를 반영하는 방법
  - makemigrations
    - model 변경값을 기반 새로운 설계도 생성
  - migrate
    - DB에 반영
  - sqlmigrate
    - SQL 구문 보기
  - showmigrations
    - 마이그레이션 상태 보기



## DB API

- class이름.objects.all()



- Manager
  - django 모델에 데이터베이스 query 작업이 제공되는 인터페이스
  - 기본적으로 모든 django 모델 클래스에 objects라는 Manager를 추가
- QuerySet
  - 데이터베이스로 부터 전달받는 객체 목록
  - 0개 1개 혹은 여러개



##  CRUD

- Create / Read / Update / Delete를 묶어서 일컫는 말



### create

1.

article = Article()

article.title = '한화이글스'

article.content = '우승은 언제...'

article.save()



2.

artcie = Article(title='한화야....', content='좀 이겨라')

article.save()



3.

Article.objects.create(title='나는', content='행복합니다.')

작성후 꼭 shell_plus 재시작해야함!



### READ

- Article.objects.all()[0]
- Article.objects.all().first()
- article = Article.objects.get(pk=100)
- Article.objects.filter(content='django!')



### UPDATE

- article = Article.objects.get(pk=1)
- article.title = 'byebye'
- article.save()



### DELETE

- article = Article.objects.get(pk=1)
- article.delete()



### lookups

- sql의 where절
- 특정 조건 적용
- __ gt = 보다 큼
- __ contains = 포함
- __ exact 정확히 일치
- __  gte 크거나 같음
- __ lt 작음
- __ lte 작거나 같음
- __ startwith 시작하는지
- __ endwith 끝나는지



## Admin Site

- 관리자가 활용하기 위한 페이지
- Article class를 admin.py에 등록
- django.contrib.auth 모듈에서 제공
- $ python manage.py createsueruser
- admin.site.register(Article)
  - admin.py에 등록

